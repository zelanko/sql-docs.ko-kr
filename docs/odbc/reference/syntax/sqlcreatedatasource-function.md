---
title: SQLCreateDataSource 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b3a6fced096c779b5ab91bf4e5b6a3f0a66e5f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68121394"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 함수
**규칙**  
 소개 된 버전: ODBC 2.0  
  
 **요약**  
 **Sqlcreatedatasource** 사용자가 데이터 소스를 추가할 수 있는 대화 상자를 표시 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>인수  
 *hwnd*  
 입력 부모 창 핸들입니다.  
  
 *lpszDS*  
 입력 데이터 원본 이름입니다. *lpszDS* 은 null 포인터 또는 빈 문자열일 수 있습니다.  
  
## <a name="returns"></a>반환  
 **Sqlcreatedatasource** 는 데이터 원본이 생성 된 경우 TRUE를 반환 합니다. 그렇지 않으면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlcreatedatasource** 가 FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못 되었습니다.|*Hwnd* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_INVALID_DSN|잘못 된 DSN|*LpszDS* 인수에 DSN에 대해 잘못 된 문자열이 포함 되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|ODBC_ADD_DSN 옵션으로 **ConfigDSN** 를 호출 하지 못했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_USER_CANCELED|사용자가 작업을 취소 했습니다.|사용자가 새 데이터 원본 만들기를 취소 했습니다.|  
|ODBC_ERROR_CREATE_DSN_FAILED|요청한 DSN을 만들 수 없습니다.|데이터베이스에 연결할 수 없습니다. 파일 DSN에 대 한 **SQLDriverConnect** 호출에서 성공적인 연결을 반환 하지 않았습니다.<br /><br /> 파일에 쓸 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 *Hwnd* 가 Null 이면 **SQLCREATEDATASOURCE** 는 FALSE를 반환 합니다. 그렇지 않으면 다음 그림과 같이 설정할 데이터 원본 유형을 선택할 수 있는 마법사 페이지가 포함 된 **새 데이터 원본 만들기** 대화 상자가 표시 됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 형식 선택](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 기본 옵션은 **파일 데이터 원본**입니다. 데이터 원본을 선택 하 고 **다음** 을 클릭 하면 설치 된 드라이버 목록이 포함 된 다음 마법사 페이지가 표시 됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 드라이버 선택](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 **취소** 를 클릭 하면 대화 상자가 사라지고 **sqlcreatedatasource** 는 ODBC_ERROR_USER_CANCELED 오류 코드와 함께 FALSE를 반환 합니다. **사용자 데이터 원본** 또는 **시스템 데이터 원본** 옵션을 선택한 경우 **고급** 단추를 사용할 수 없습니다.  
  
 **다음** 단추를 클릭 하면 선택한 데이터 원본 유형에 따라 다음 중 하나가 발생 합니다.  
  
-   **파일 데이터 원본** 을 선택한 경우 사용자가 파일 이름을 입력할 수 있도록 마법사 페이지가 표시 됩니다.  
  
-   **사용자 데이터** 원본 또는 **시스템 데이터 원본** 중 하나를 선택한 경우 데이터 원본 및 드라이버 유형을 표시 하는 마법사 페이지가 검토를 위해 표시 되 고, **마침** 을 클릭 하면 데이터 원본이 설정 됩니다.  
  
 새 데이터 원본 만들기 마법사 페이지에서 **고급** 을 클릭 하면 사용자에 게 드라이버별 정보를 입력할 수 있는 마법사 페이지가 표시 됩니다. 이 대화 상자의 텍스트 상자에 다음 그림과 같이로 구분 된 드라이버 및 키워드를 입력 합니다.  
  
 ![파일 DSN 만들기 고급 설정 대화 상자](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 **SQLDriverConnect**에 대 한 설명에서 추가 드라이버별 키워드를 찾을 수 있습니다. **DSN** 을 제외한 모든를 사용할 수 있습니다.  
  
 **이 연결 확인** 옵션의 기본값은 TRUE입니다. 이 기본값은이 마법사 페이지가 활성화 되어 있는지 여부에 관계 없이 적용 됩니다. **확인** 을 클릭 하면 텍스트 상자에 지정 된 문자열과 **이 연결 확인** 옵션 값이 캐시 됩니다. [ **닫기** ] 단추 또는 **[취소** ]를 클릭 하면 텍스트 상자에 지정 된 문자열과 **이 연결 옵션 확인 값이** 캐시 되지 않으므로 새로 입력 한 드라이버 관련 정보가 모두 손실 됩니다.  
  
 첫 번째 마법사 페이지에서 **파일 데이터 원본을** 선택한 경우 드라이버를 선택 하 고 고급 마법사 페이지에서 키워드 값을 입력 한 후에는 파일 이름을 입력 하 라는 메시지가 표시 됩니다. **찾아보기** 를 클릭 하 여 파일 이름을 검색 합니다 .이 경우 **찾아보기** 상자의 기본 디렉터리는 HKEY_LOCAL_MACHINE \software\microsoft\windows\currentversion 및 "ODBC\DataSources"에서 CommonFileDir에 지정 된 경로 조합으로 지정 됩니다. CommonFileDir가 "C:\Program Files\Common Files" 인 경우 기본 디렉터리는 "C:\Program Files\Common Files\ODBC\Data Sources"입니다.  
  
 파일 이름을 입력 하 고 **다음** 을 클릭 하면 입력 된 파일 이름에 운영 체제의 표준 파일 이름 지정 규칙에 대 한 유효성 검사가 수행 됩니다. 파일 이름이 잘못 된 경우 오류 메시지 상자는 잘못 된 파일 이름을 입력 했음을 사용자에 게 알려 줍니다. 사용자가 메시지 상자를 승인한 후에 파일 이름을 입력 하는 마법사 페이지로 포커스가 반환 됩니다. 파일 이름이 유효한 경우 다음 그림에 표시 된 것 처럼 검토를 위해 선택한 키워드-값 쌍을 보여 주는 마법사 페이지가 표시 됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 검토](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 **마침** 을 클릭 하 고 **파일 데이터 원본이** 데이터 원본 유형으로 선택 된 경우 **이 연결 확인** 옵션이 TRUE 이면 **SAVEFILE** 및 **DRIVER** 키워드를 사용 하 여 **SQLDriverConnect** 이 호출 됩니다. *Drivercompletion* 인수가 SQL_DRIVER_COMPLETE로 설정 되어 있습니다. **SAVEFILE** 키워드의 파일 이름은 입력 하거나 선택한 이름 이며 **driver** 키워드의 드라이버 이름은 선택한 이름입니다. 고급 마법사 페이지에서 드라이버별 연결 문자열이 지정 된 경우 해당 문자열은 **driver** 키워드 뒤에 추가 됩니다.  
  
 **SQLDriverConnect** 가 SQL_SUCCESS을 반환 하는 경우 드라이버 관리자가 파일 DSN을 만들었습니다. **Sqlcreatedatasource** 는 TRUE를 반환 합니다. **SQLDriverConnect** 가 SQL_SUCCESS 반환 하지 않으면 데이터 원본에 연결할 수 없다는 경고 메시지 상자가 표시 됩니다. 최소한의 연결 정보를 포함 하는 DSN은 계속 만들 수 있습니다. 이 메시지 상자를 사용 하면 사용자가 파일 DSN 만들기를 취소 하거나 계속 진행할 수 있습니다.  
  
 사용자가 DSN을 계속 만들도록 선택 하는 경우이 **연결 확인** 옵션이 FALSE로 설정 된 것 처럼이 프로세스가 계속 됩니다. 사용자가 취소를 선택 하면 ODBC_ERROR_CREATE_DSN_FAILED 오류 코드와 함께 **Sqlcreatedatasource** 에 대해 FALSE가 반환 됩니다.  
  
 **파일 데이터 원본을** 데이터 원본 유형으로 선택 하 고 **이 연결 확인** 옵션이 FALSE 인 경우 고급 마법사 페이지에서 **DRIVER** 키워드 및 사용자 지정 연결 문자열 (있는 경우)을 사용 하 여 파일 DSN을 만듭니다. 파일을 만드는 데 성공한 경우 **Sqlcreatedatasource**에 대해 TRUE가 반환 됩니다. 파일 만들기에 실패 한 경우 오류 메시지 상자는 운영 체제에서 반환 된 모든 오류를 사용자에 게 알립니다. ODBC_ERROR_CREATE_DSN_FAILED 오류 코드와 함께 **Sqlcreatedatasource** 에 대해 FALSE가 반환 됩니다. 파일 데이터 원본에 대 한 자세한 내용은 [파일 데이터 원본을 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)를 참조 하세요.  
  
 **사용자** 또는 **시스템 데이터 원본이** 데이터 원본 유형으로 선택 된 경우 드라이버 설치 라이브러리의 **ConfigDSN** 가 ODBC_ADD_DSN *frequest*를 사용 하 여 호출 됩니다. 자세한 내용은 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본 관리|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
