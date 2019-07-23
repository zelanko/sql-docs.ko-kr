---
title: 사용자 지정 키 저장소 공급자 | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: 0cf2946517be732094d01ff9889faf080a36e85b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006484"
---
# <a name="custom-keystore-providers"></a>사용자 지정 키 저장소 공급자
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>개요

SQL Server 2016의 열 암호화 기능을 사용 하려면 암호화 된 열에 저장 된 데이터에 액세스 하기 위해 서버에 저장 된 암호화 된 열 암호화 키 (ECEKs)를 클라이언트에서 검색 한 다음 CEKs (열 암호화 키)로 해독 해야 합니다. ECEKs는 CMKs (열 마스터 키)로 암호화 되며, CMKS의 보안은 열 암호화의 보안에 중요 합니다. 따라서 CMK는 안전한 위치에 저장 해야 합니다. 열 암호화 키 저장소 공급자는 ODBC 드라이버가 안전 하 게 저장 된 CMKs에 액세스할 수 있도록 인터페이스를 제공 합니다. 사용자 지정 보안 저장소를 사용 하는 사용자의 경우 사용자 지정 키 저장소 공급자 인터페이스는 ODBC 드라이버에 대 한 CMK의 보안 저장소에 대 한 액세스를 구현 하기 위한 프레임 워크를 제공 하며,이를 사용 하 여 CEK 암호화 및 암호 해독을 수행할 수 있습니다.

각 키 저장소 공급자는 하나 이상의 CMKs를 포함 하 고 관리 합니다. 하나 이상의 CMKs는 공급자에서 정의한 형식의 키 경로에 의해 식별 됩니다. 이는 암호화 알고리즘과 함께 공급자에 의해 정의 된 문자열을 사용 하 여 CEK의 암호화 및 ECEK의 암호 해독을 수행할 수 있습니다. 이 알고리즘은 ECEK와 공급자의 이름과 함께 데이터베이스의 암호화 메타 데이터에 저장 됩니다. 자세한 내용은 [열 마스터 키 만들기](../../t-sql/statements/create-column-master-key-transact-sql.md) 및 [열 암호화 키 만들기](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 를 참조 하세요. 따라서 키 관리의 두 가지 기본 작업은 다음과 같습니다.

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

여기서는 `CEKeystoreProvider_name` 특정 열 Encryption 키 저장소 provider (cekeyvault 공급자)를 식별 하는 데 사용 되 고, 다른 인수는 cekeyvault 공급자가 (E) CEK을 암호화/해독 하는 데 사용 됩니다. Name 및 keypath는 CMK 메타 데이터에서 제공 하는 반면, algorithm 및 ECEK 값은 CEK 메타 데이터에서 제공 됩니다. 기본 제공 공급자와 함께 여러 키 저장소 공급자가 있을 수 있습니다. CEK가 필요한 작업을 수행 하는 경우 드라이버는 CMK 메타 데이터를 사용 하 여 이름으로 적절 한 키 저장소 공급자를 찾고 다음과 같이 표시할 수 있는 해독 작업을 실행 합니다.

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

드라이버가 CEKs를 암호화할 필요가 없지만 CMK 만들기 및 회전과 같은 작업을 구현 하기 위해 키 관리 도구에서이 작업을 수행 해야 할 수도 있습니다. 이렇게 하려면 역 작업을 수행 해야 합니다.

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>Cekeyvault 공급자 인터페이스

이 문서에서는 Cekeyvault 공급자 인터페이스에 대해 자세히 설명 합니다. 이 인터페이스를 구현 하는 키 저장소 공급자는 Microsoft ODBC Driver for SQL Server 사용할 수 있습니다. Cekeyvault 공급자 구현자는이 가이드를 사용 하 여 드라이버에서 사용할 수 있는 사용자 지정 키 저장소 공급자를 개발할 수 있습니다.

키 저장소 공급자 라이브러리 ("공급자 라이브러리")는 ODBC 드라이버에서 로드할 수 있고 하나 이상의 키 저장소 공급자를 포함 하는 동적 연결 라이브러리입니다. 기호 `CEKeystoreProvider` 는 공급자 라이브러리에서 내보내야 하며, 라이브러리 내의 각 키 저장소 공급자에 대 한 구조체에 `CEKeystoreProvider` 대 한 포인터의 null로 끝나는 배열 주소 여야 합니다.

구조 `CEKeystoreProvider` 는 단일 키 저장소 공급자의 진입점을 정의 합니다.

```
typedef struct CEKeystoreProvider {
    wchar_t *Name;
    int (*Init)(CEKEYSTORECONTEXT *ctx, errFunc *onError);
    int (*Read)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int *len);
    int (*Write)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len);
    int (*DecryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *ecek,
                        unsigned short ecekLen,
                        unsigned char **cekOut,
                        unsigned short *cekLen);
    int (*EncryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *cek,
                        unsigned short cekLen,
                        unsigned char **ecekOut,
                        unsigned short *ecekLen);
    void (*Free)();
} CEKEYSTOREPROVIDER;
```

|필드 이름|설명|
|:--|:--|
|`Name`|키 저장소 공급자의 이름입니다. 이전에 드라이버에서 로드 했거나이 라이브러리에 있는 다른 키 저장소 공급자와 같지 않아야 합니다. Null로 종료된 와이드 문자*열입니다.|
|`Init`|초기화 함수 초기화 함수가 필요 하지 않은 경우이 필드는 null 일 수 있습니다.|
|`Read`|공급자 읽기 함수입니다. 필요 하지 않은 경우 null 일 수 있습니다.|
|`Write`|공급자 쓰기 함수입니다. Read가 null이 아닌 경우 필요 합니다. 필요 하지 않은 경우 null 일 수 있습니다.|
|`DecryptCEK`|ECEK 암호 해독 함수 이 함수는 키 저장소 공급자가 존재 하는 이유 이며 null이 아니어야 합니다.|
|`EncryptCEK`|CEK 암호화 함수입니다. 드라이버는이 함수를 호출 하지 않지만 키 관리 도구를 사용 하 여 ECEK 생성에 프로그래밍 방식으로 액세스할 수 있습니다. 필요 하지 않은 경우 null 일 수 있습니다.|
|`Free`|종료 함수입니다. 필요 하지 않은 경우 null 일 수 있습니다.|

Free를 제외 하 고이 인터페이스의 함수에는 모두 **ctx** 및 **onError**매개 변수 쌍이 있습니다. 이전에는 함수가 호출 되는 컨텍스트를 식별 하는 반면 후자는 오류를 보고 하는 데 사용 됩니다. 자세한 내용은 아래의 [컨텍스트](#context-association) 및 [오류 처리](#error-handling) 를 참조 하세요.

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
공급자 정의 초기화 함수의 자리 표시자 이름입니다. 공급자가 로드 된 후, 처음으로 ECEK 암호 해독 또는 읽기 ()/쓰기 () 요청을 수행 해야 하는 경우 드라이버는이 함수를 한 번 호출 합니다. 이 함수를 사용 하 여 필요한 초기화를 수행 합니다. 

|인수|설명|
|:--|:--|
|`ctx`|입력 작업 컨텍스트입니다.|
|`onError`|입력 오류 보고 함수입니다.|
|`Return Value`|성공 여부를 나타내려면 0이 아닌 값을 반환 하 고, 실패를 나타내려면 0을 반환 합니다.|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

공급자 정의 통신 함수의 자리 표시자 이름입니다. 응용 프로그램에서 SQL_COPT_SS_CEKEYSTOREDATA 연결 특성을 사용 하 여 (이전에 작성 한) 공급자의 데이터를 읽으려고 할 때 드라이버가이 함수를 호출 하 여 응용 프로그램에서 공급자의 임의 데이터를 읽을 수 있게 합니다. 자세한 내용은 [키 저장소 공급자와 통신](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) 을 참조 하세요.

|인수|설명|
|:--|:--|
|`ctx`|입력 작업 컨텍스트입니다.|
|`onError`|입력 오류 보고 함수입니다.|
|`data`|출력 응용 프로그램에서 읽을 데이터를 공급자가 기록 하는 버퍼에 대 한 포인터입니다. 이는 CEKEYVAULT 데이터 구조의 데이터 필드에 해당 합니다.|
|`len`|InOut 길이 값에 대 한 포인터입니다. 입력 시이는 데이터 버퍼의 최대 길이 이며 공급자는 * len 바이트를 초과 하 여 쓰지 않아야 합니다. 반환 시 공급자는 실제로 쓰여진 바이트 수로 * len을 업데이트 해야 합니다.|
|`Return Value`|성공 여부를 나타내려면 0이 아닌 값을 반환 하 고, 실패를 나타내려면 0을 반환 합니다.|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
공급자 정의 통신 함수의 자리 표시자 이름입니다. 응용 프로그램이 SQL_COPT_SS_CEKEYSTOREDATA 연결 특성을 사용 하 여 데이터를 공급자에 쓰려고 할 때 드라이버가이 함수를 호출 하 여 응용 프로그램이 임의의 데이터를 공급자에 게 쓸 수 있도록 합니다. 자세한 내용은 [키 저장소 공급자와 통신](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) 을 참조 하세요.

|인수|설명|
|:--|:--|
|`ctx`|입력 작업 컨텍스트입니다.|
|`onError`|입력 오류 보고 함수입니다.|
|`data`|입력 읽을 공급자의 데이터를 포함 하는 버퍼에 대 한 포인터입니다. 이는 CEKEYVAULT 데이터 구조의 데이터 필드에 해당 합니다. 공급자는이 버퍼에서 len 바이트를 초과 하지 않아야 합니다.|
|`len`|입력 데이터에서 사용할 수 있는 바이트 수입니다. 이는 CEKEYDATASIZE 데이터 구조의 dataSize 필드에 해당 합니다.|
|`Return Value`|성공 여부를 나타내려면 0이 아닌 값을 반환 하 고, 실패를 나타내려면 0을 반환 합니다.|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
공급자가 정의한 ECEK 암호 해독 함수의 자리 표시자 이름입니다. 드라이버는이 함수를 호출 하 여이 공급자와 연결 된 CMK가 CEK로 암호화 된 ECEK의 암호를 해독 합니다.

|인수|설명|
|:--|:--|
|`ctx`|입력 작업 컨텍스트입니다.|
|`onError`|입력 오류 보고 함수입니다.|
|`keyPath`|입력 지정 된 ECEK에서 참조 하는 CMK에 대 한 [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) metadata 특성의 값입니다. Null로 종료된 와이드 문자*열입니다. 이 공급자가 처리 하는 CMK를 식별 하기 위한 것입니다.|
|`alg`|입력 지정 된 ECEK에 대 한 [알고리즘](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 메타 데이터 특성의 값입니다. Null로 종료된 와이드 문자*열입니다. 이는 지정 된 ECEK를 암호화 하는 데 사용 되는 암호화 알고리즘을 식별 하기 위한 것입니다.|
|`ecek`|입력 암호를 해독할 ECEK에 대 한 포인터입니다.|
|`ecekLen`|입력 ECEK의 길이입니다.|
|`cekOut`|출력 공급자는 해독 된 ECEK에 대해 메모리를 할당 하 고 cekOut에서 가리키는 포인터에 해당 주소를 씁니다. [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 또는 Free (Linux/Mac) 함수를 사용 하 여이 메모리 블록을 해제할 수 있어야 합니다. 오류가 발생 하거나 다른 방법으로 인해 메모리가 할당 되지 않은 경우 공급자는 * cekOut을 null 포인터로 설정 해야 합니다.|
|`cekLen`|출력 공급자는 * * Ceklen에 기록한 해독 된 ECEK의 길이를 cekLen에서 가리키는 주소에 써야 합니다.|
|`Return Value`|성공 여부를 나타내려면 0이 아닌 값을 반환 하 고, 실패를 나타내려면 0을 반환 합니다.|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
공급자 정의 CEK 암호화 함수의 자리 표시자 이름입니다. 드라이버는이 함수를 호출 하거나 ODBC 인터페이스를 통해 해당 기능을 노출 하지 않지만 키 관리 도구를 사용 하 여 ECEK 생성에 프로그래밍 방식으로 액세스할 수 있습니다.

|인수|설명|
|:--|:--|
|`ctx`|입력 작업 컨텍스트입니다.|
|`onError`|입력 오류 보고 함수입니다.|
|`keyPath`|입력 지정 된 ECEK에서 참조 하는 CMK에 대 한 [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) metadata 특성의 값입니다. Null로 종료된 와이드 문자*열입니다. 이 공급자가 처리 하는 CMK를 식별 하기 위한 것입니다.|
|`alg`|입력 지정 된 ECEK에 대 한 [알고리즘](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 메타 데이터 특성의 값입니다. Null로 종료된 와이드 문자*열입니다. 이는 지정 된 ECEK를 암호화 하는 데 사용 되는 암호화 알고리즘을 식별 하기 위한 것입니다.|
|`cek`|입력 암호화할 CEK에 대 한 포인터입니다.|
|`cekLen`|입력 CEK의 길이입니다.|
|`ecekOut`|출력 공급자는 암호화 된 CEK에 대해 메모리를 할당 하 고 ecekOut가 가리키는 포인터에 해당 주소를 씁니다. [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) 또는 Free (Linux/Mac) 함수를 사용 하 여이 메모리 블록을 해제할 수 있어야 합니다. 오류가 발생 하거나 다른 방법으로 인해 메모리가 할당 되지 않은 경우 공급자는 * ecekOut을 null 포인터로 설정 해야 합니다.|
|`ecekLen`|출력 공급자는 * * ecekOut에 기록한 암호화 된 CEK의 길이를 ecekLen 하 여 가리키는 주소에 써야 합니다.|
|`Return Value`|성공 여부를 나타내려면 0이 아닌 값을 반환 하 고, 실패를 나타내려면 0을 반환 합니다.|

```
void (*Free)();
```
공급자 정의 종료 함수의 자리 표시자 이름입니다. 프로세스가 정상적으로 종료 되 면 드라이버에서이 함수를 호출할 수 있습니다.

> [!NOTE]
> *와이드 문자 문자열은 SQL Server 저장 하는 방법 때문에 2 바이트 문자 (UTF-16)입니다.*


### <a name="error-handling"></a>오류 처리

공급자를 처리 하는 동안 오류가 발생할 수 있으므로 부울 성공/실패와 관련 하 여 오류를 드라이버에 다시 보고할 수 있는 메커니즘이 제공 됩니다. 대부분의 함수에는 성공/실패 반환 값 외에도이 목적으로 함께 사용 되는 **ctx** 및 **onError**매개 변수 쌍이 있습니다.

**Ctx** 매개 변수는 공급자 작업이 발생 하는 컨텍스트를 식별 합니다.

**OnError** 매개 변수는 다음 프로토타입을 사용 하 여 오류 보고 함수를 가리킵니다.

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|인수|설명|
|:--|:--|
|`ctx`|입력 오류를 보고할 컨텍스트입니다.|
|`msg`|입력 보고할 오류 메시지입니다. Null로 종료된 와이드 문자열입니다. 매개 변수가 있는 정보를 제공 하도록 허용 하려면이 문자열에 [FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage) 함수에서 허용 하는 형식의 삽입 형식 지정 시퀀스가 포함 될 수 있습니다. 확장 된 기능은 아래에 설명 된 대로이 매개 변수로 지정할 수 있습니다.|
|...|입력 필요에 따라 메시지의 형식 지정자에 맞는 추가 variadic 매개 변수입니다.|

오류가 발생 한 경우를 보고 하기 위해 공급자는 onError를 호출 하 여 공급자 함수에 전달 된 컨텍스트 매개 변수를 드라이버에 전달 하 고 선택적으로 추가 매개 변수를 지정할 수 있는 오류 메시지를 제공 합니다. 공급자는이 함수를 여러 번 호출 하 여 한 공급자 함수 호출 내에 여러 오류 메시지를 연속적으로 게시할 수 있습니다. 예를 들어

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


`msg` 매개 변수는 일반적으로 와이드 문자 문자열 이지만 추가 확장을 사용할 수 있습니다.

IDS_MSG 매크로를 사용 하 여 미리 정의 된 특수 값 중 하나를 사용 하 여 기존 및 드라이버의 localised 형식에 일반적인 오류 메시지를 활용할 수 있습니다. 예를 들어 공급자가 메모리 `IDS_S1_001` 할당에 실패 하면 "메모리 할당 오류" 메시지를 사용할 수 있습니다.

`onError(ctx, IDS_MSG(IDS_S1_001));`

드라이버에서 오류를 failedodatapropertyname 공급자 함수는 오류를 반환 해야 합니다. Odbc 작업의 컨텍스트에서 수행 되는 경우 게시 된 오류는 표준 ODBC 진단 메커니즘 (`SQLError`, `SQLGetDiagRec`및 `SQLGetDiagField`)을 통해 연결 또는 문 핸들에서 액세스할 수 있게 됩니다.


### <a name="context-association"></a>컨텍스트 연결

구조 `CEKEYSTORECONTEXT` 는 오류 콜백에 대 한 컨텍스트를 제공 하는 것 외에도 공급자 작업이 실행 되는 ODBC 컨텍스트를 결정 하는 데 사용할 수 있습니다. 이렇게 하면 공급자가 이러한 각 컨텍스트에 데이터를 연결할 수 있습니다. 예를 들어 연결 단위 구성을 구현 합니다. 이러한 목적을 위해 구조에는 환경, 연결 및 문 컨텍스트에 해당 하는 3 개의 불투명 포인터가 포함 됩니다.

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```

|필드|설명|
|:--|:--|
|`envCtx`|환경 컨텍스트입니다.|
|`dbcCtx`|연결 컨텍스트입니다.|
|`stmtCtx`|문 컨텍스트입니다.|

이러한 각 컨텍스트는 불투명 값으로, 해당 ODBC 핸들과 동일 하지 않지만 핸들의 고유 식별자로 사용할 수 있습니다. 즉, 핸들 *X* 가 컨텍스트 값 *Y*와 연결 된 경우 다른 환경, 연결 또는 *x* 와 동일한 시간에 동시에 존재 하는 문 핸들은 *Y*의 컨텍스트 값을 가지 며, 다른 컨텍스트 값은 핸들 *X*와 연결 되지 않습니다. 수행 중인 공급자 작업에 특정 핸들 컨텍스트가 없는 경우 (예: SQLSetConnectAttr를 호출 하 여 문 핸들이 없는 공급자를 로드 하 고 구성 하는 경우) 구조체의 해당 컨텍스트 값은 null입니다.


## <a name="example"></a>예제

### <a name="keystore-provider"></a>키 저장소 공급자

다음 코드는 최소 키 저장소 공급자 구현의 예입니다.

```
/* Custom Keystore Provider Example

Windows:   compile with cl MyKSP.c /LD /MD /link /out:MyKSP.dll
Linux/Mac: compile with gcc -fshort-wchar -fPIC -o MyKSP.so -shared MyKSP.c

 */

#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#endif

#include <stdlib.h>
#include <sqltypes.h>
#include "msodbcsql.h"
#include <sql.h>
#include <sqlext.h>

int __stdcall KeystoreInit(CEKEYSTORECONTEXT *ctx, errFunc *onError) {
    printf("KSP Init() function called\n");
    return 1;
}

static unsigned char *g_encryptKey;
static unsigned int g_encryptKeyLen;

int __stdcall KeystoreWrite(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len) {
    printf("KSP Write() function called (%d bytes)\n", len);
    if (len) {
        if (g_encryptKey)
            free(g_encryptKey);
        g_encryptKey = malloc(len);
        if (!g_encryptKey) {
            onError(ctx, L"Memory Allocation Error");
            return 0;
        }
        memcpy(g_encryptKey, data, len);
        g_encryptKeyLen = len;
    }
    return 1;
}

// Very simple "encryption" scheme - rotating XOR with the key
int __stdcall KeystoreDecrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg,
    unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen) {
    unsigned int i;
    printf("KSP Decrypt() function called (keypath=%S alg=%S ecekLen=%u)\n", keyPath, alg, ecekLen);
    if (wcscmp(keyPath, L"TheOneAndOnlyKey")) {
        onError(ctx, L"Invalid key path");
        return 0;
    }
    if (wcscmp(alg, L"none")) {
        onError(ctx, L"Invalid algorithm");
        return 0;
    }
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
#ifndef _WIN32
    *cekOut = malloc(ecekLen);
#else
    *cekOut = LocalAlloc(LMEM_FIXED, ecekLen);
#endif
    if (!*cekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *cekLen = ecekLen;
    for (i = 0; i < ecekLen; i++)
        (*cekOut)[i] = ecek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

// Note that in the provider interface, this function would be referenced via the CEKEYSTOREPROVIDER
// structure. However, that does not preclude keystore providers from exporting their own functions,
// as illustrated by this example where the encryption is performed via a separate function (with a
// different prototype than the one in the KSP interface.)
#ifdef _WIN32
__declspec(dllexport)
#endif
int KeystoreEncrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError,
    unsigned char *cek, unsigned short cekLen,
    unsigned char **ecekOut, unsigned short *ecekLen) {
    unsigned int i;
    printf("KSP Encrypt() function called (cekLen=%u)\n", cekLen);
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
    *ecekOut = malloc(cekLen);
    if (!*ecekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *ecekLen = cekLen;
    for (i = 0; i < cekLen; i++)
        (*ecekOut)[i] = cek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

CEKEYSTOREPROVIDER MyCustomKSPName_desc = {
    L"MyCustomKSPName",
    KeystoreInit,
    0,
    KeystoreWrite,
    KeystoreDecrypt,
    0
};

#ifdef _WIN32
__declspec(dllexport)
#endif
CEKEYSTOREPROVIDER *CEKeystoreProvider[] = {
    &MyCustomKSPName_desc,
    0
};
```

### <a name="odbc-application"></a>ODBC 응용 프로그램

다음 코드는 위의 키 저장소 공급자를 사용 하는 데모 응용 프로그램입니다. 이를 실행 하는 경우 공급자 라이브러리가 응용 프로그램 이진 파일의 디렉터리와 동일한 디렉터리에 있는지 확인 하 고, 연결 문자열에서 해당 `ColumnEncryption=Enabled` 설정이 포함 된 DSN을 지정 하거나 지정 합니다.

```
/*
 Example application for demonstration of custom keystore provider usage

Windows:   compile with cl /MD kspapp.c /link odbc32.lib
Linux/Mac: compile with gcc -o kspapp -fshort-wchar kspapp.c -lodbc -ldl
 
 usage: kspapp connstr

 */

#define KSPNAME L"MyCustomKSPName"
#define PROV_ENCRYPT_KEY "JHKCWYT06N3RG98J0MBLG4E3"

#include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#include <dlfcn.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include "msodbcsql.h"

/* Convenience functions */

int checkRC(SQLRETURN rc, char *msg, int ret, SQLHANDLE h, SQLSMALLINT ht) {
    if (rc == SQL_ERROR) {
        fprintf(stderr, "Error occurred upon %s\n", msg);
        if (h) {
            SQLSMALLINT i = 0;
            SQLSMALLINT outlen = 0;
            char errmsg[1024];
            while ((rc = SQLGetDiagField(
                ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
                || rc == SQL_SUCCESS_WITH_INFO) {
                fprintf(stderr, "Err#%d: %s\n", i, errmsg);
            }
        }
        if (ret)
            exit(ret);
        return 0;
    }
    else if (rc == SQL_SUCCESS_WITH_INFO && h) {
        SQLSMALLINT i = 0;
        SQLSMALLINT outlen = 0;
        char errmsg[1024];
        printf("Success with info for %s:\n", msg);
        while ((rc = SQLGetDiagField(
            ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
            || rc == SQL_SUCCESS_WITH_INFO) {
            fprintf(stderr, "Msg#%d: %s\n", i, errmsg);
        }
    }
    return 1;
}

void postKspError(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...) {
    if (msg > (wchar_t*)65535)
        wprintf(L"Provider emitted message: %s\n", msg);
    else
        wprintf(L"Provider emitted message ID %d\n", msg);
}

int main(int argc, char **argv) {
    char sqlbuf[1024];
    SQLHENV env;
    SQLHDBC dbc;
    SQLHSTMT stmt;
    SQLRETURN rc;
    unsigned char CEK[32];
    unsigned char *ECEK;
    unsigned short ECEKlen;
#ifdef _WIN32
    HMODULE hProvLib;
#else
    void *hProvLib;
#endif
    CEKEYSTORECONTEXT ctx = {0};
    CEKEYSTOREPROVIDER **ppKsp, *pKsp;
    int(__stdcall *pEncryptCEK)(CEKEYSTORECONTEXT *, errFunc *, unsigned char *, unsigned short, unsigned char **, unsigned short *);
    int i;
    if (argc < 2) {
        fprintf(stderr, "usage: kspapp connstr\n");
        return 1;
    }

    /* Load the provider library */
#ifdef _WIN32
    if (!(hProvLib = LoadLibrary("MyKSP.dll"))) {
#else
    if (!(hProvLib = dlopen("./MyKSP.so", RTLD_NOW))) {
#endif
        fprintf(stderr, "Error loading KSP library\n");
        return 2;
    }
#ifdef _WIN32
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)GetProcAddress(hProvLib, "CEKeystoreProvider"))) {
#else
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)dlsym(hProvLib, "CEKeystoreProvider"))) {
#endif
        fprintf(stderr, "The export CEKeystoreProvider was not found in the KSP library\n");
        return 3;
    }
    while (pKsp = *ppKsp++) {
        if (!memcmp(KSPNAME, pKsp->Name, sizeof(KSPNAME)))
            goto FoundProv;
    }
    fprintf(stderr, "Could not find provider in the library\n");
    return 4;
FoundProv:
    if (pKsp->Init && !pKsp->Init(&ctx, postKspError)) {
        fprintf(stderr, "Could not initialize provider\n");
        return 5;
    }
#ifdef _WIN32
    if (!(pEncryptCEK = (LPVOID)GetProcAddress(hProvLib, "KeystoreEncrypt"))) {
#else
    if (!(pEncryptCEK = dlsym(hProvLib, "KeystoreEncrypt"))) {
#endif
        fprintf(stderr, "The export KeystoreEncrypt was not found in the KSP library\n");
        return 6;
    }
    if (!pKsp->Write) {
        fprintf(stderr, "Provider does not support configuration\n");
        return 7;
    }

    /* Configure the provider with the key */
    if (!pKsp->Write(&ctx, postKspError, PROV_ENCRYPT_KEY, strlen(PROV_ENCRYPT_KEY))) {
        fprintf(stderr, "Error writing to KSP\n");
        return 8;
    }

    /* Generate a CEK and encrypt it with the provider */
    srand(time(0) ^ getpid());
    for (i = 0; i < sizeof(CEK); i++)
        CEK[i] = rand();

    if (!pEncryptCEK(&ctx, postKspError, CEK, sizeof(CEK), &ECEK, &ECEKlen)) {
        fprintf(stderr, "Error encrypting CEK\n");
        return 9;
    }

    /* Connect to Server */
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &env);
    checkRC(rc, "allocating environment handle", 2, 0, 0);
    rc = SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);
    checkRC(rc, "setting ODBC version to 3.0", 3, env, SQL_HANDLE_ENV);
    rc = SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc);
    checkRC(rc, "allocating connection handle", 4, env, SQL_HANDLE_ENV);
    rc = SQLDriverConnect(dbc, 0, argv[1], strlen(argv[1]), NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    checkRC(rc, "connecting to data source", 5, dbc, SQL_HANDLE_DBC);
    rc = SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt);
    checkRC(rc, "allocating statement handle", 6, dbc, SQL_HANDLE_DBC);

    /* Create a CMK definition on the server */
    {
        static char cmkSql[] = "CREATE COLUMN MASTER KEY CustomCMK WITH ("
            "KEY_STORE_PROVIDER_NAME = 'MyCustomKSPName',"
            "KEY_PATH = 'TheOneAndOnlyKey')";
        printf("Create CMK: %s\n", cmkSql);
        SQLExecDirect(stmt, cmkSql, SQL_NTS);
    }

    /* Create a CEK definition on the server */
    {
        const char cekSqlBefore[] = "CREATE COLUMN ENCRYPTION KEY CustomCEK WITH VALUES ("
            "COLUMN_MASTER_KEY = CustomCMK,"
            "ALGORITHM = 'none',"
            "ENCRYPTED_VALUE = 0x";
        char *cekSql = malloc(sizeof(cekSqlBefore) + 2 * ECEKlen + 2); /* 1 for ')', 1 for null terminator */
        strcpy(cekSql, cekSqlBefore);
        for (i = 0; i < ECEKlen; i++)
            sprintf(cekSql + sizeof(cekSqlBefore) - 1 + 2 * i, "%02x", ECEK[i]);
        strcat(cekSql, ")");
        printf("Create CEK: %s\n", cekSql);
        SQLExecDirect(stmt, cekSql, SQL_NTS);
        free(cekSql);
#ifdef _WIN32
        LocalFree(ECEK);
#else
        free(ECEK);
#endif
    }

#ifdef _WIN32
    FreeLibrary(hProvLib);
#else
    dlclose(hProvLib);
#endif

    /* Create a table with encrypted columns */
    {
        static char *tableSql = "CREATE TABLE CustomKSPTestTable ("
            "c1 int,"
            "c2 varchar(255) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CustomCEK, ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'))";
        printf("Create table: %s\n", tableSql);
        SQLExecDirect(stmt, tableSql, SQL_NTS);
    }

    /* Load provider into the ODBC Driver and configure it */
    {
        unsigned char ksd[sizeof(CEKEYSTOREDATA) + sizeof(PROV_ENCRYPT_KEY) - 1];
        CEKEYSTOREDATA *pKsd = (CEKEYSTOREDATA*)ksd;
        pKsd->name = L"MyCustomKSPName";
        pKsd->dataSize = sizeof(PROV_ENCRYPT_KEY) - 1;
        memcpy(pKsd->data, PROV_ENCRYPT_KEY, sizeof(PROV_ENCRYPT_KEY) - 1);
#ifdef _WIN32
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "MyKSP.dll", SQL_NTS);
#else
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "./MyKSP.so", SQL_NTS);
#endif
        checkRC(rc, "Loading KSP into ODBC Driver", 7, dbc, SQL_HANDLE_DBC);
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREDATA, (SQLPOINTER)pKsd, SQL_IS_POINTER);
        checkRC(rc, "Configuring the KSP", 7, dbc, SQL_HANDLE_DBC);
    }

    /* Insert some data */
    {
        int c1;
        char c2[256];
        rc = SQLBindParameter(stmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 0, 0, &c1, 0, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        rc = SQLBindParameter(stmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 255, 0, c2, 255, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        for (i = 0; i < 10; i++) {
            c1 = i * 10 + i + 1;
            sprintf(c2, "Sample data %d for column 2", i);
            rc = SQLExecDirect(stmt, "INSERT INTO CustomKSPTestTable (c1, c2) values (?, ?)", SQL_NTS);
            checkRC(rc, "Inserting rows query", 10, stmt, SQL_HANDLE_STMT);
        }
        printf("(Encrypted) data has been inserted into the [CustomKSPTestTable]. You may inspect the data now.\n"
            "Press Enter to continue...\n");
        getchar();
    }

    /* Retrieve the data */
    {
        int c1;
        char c2[256];
        rc = SQLBindCol(stmt, 1, SQL_C_LONG, &c1, 0, 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLBindCol(stmt, 2, SQL_C_CHAR, c2, sizeof(c2), 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLExecDirect(stmt, "SELECT c1, c2 FROM CustomKSPTestTable", SQL_NTS);
        checkRC(rc, "Retrieving rows query", 12, stmt, SQL_HANDLE_STMT);
        while (SQL_SUCCESS == (rc = SQLFetch(stmt)))
            printf("Retrieved data: c1=%d c2=%s\n", c1, c2);
        SQLFreeStmt(stmt, SQL_CLOSE);
        printf("Press Enter to clean up and exit...\n");
        getchar();
    }

    /* Clean up */
    {
        SQLExecDirect(stmt, "DROP TABLE CustomKSPTestTable", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN ENCRYPTION KEY CustomCEK", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN MASTER KEY CustomCMK", SQL_NTS);
        printf("Removed table, CEK, and CMK\n");
    }
    SQLDisconnect(dbc);
    SQLFreeHandle(SQL_HANDLE_DBC, dbc);
    SQLFreeHandle(SQL_HANDLE_ENV, env);
    return 0;
}

```

## <a name="see-also"></a>참고 항목

[상시 암호화와 ODBC 드라이버 사용](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
