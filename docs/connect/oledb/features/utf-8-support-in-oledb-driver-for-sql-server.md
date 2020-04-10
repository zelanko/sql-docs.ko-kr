---
title: SQL Server용 OLE DB 드라이버에서 UTF-8 지원| Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 UTF-8 지원
ms.custom: ''
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: reference
ms.reviewer: v-kaywon
ms.author: v-daenge
author: David-Engel
ms.openlocfilehash: c18870d1d252ba849e11ce0bd040bbce89bd5855
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928272"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에서 UTF-8 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

SQL Server용 Microsoft OLE DB 드라이버(버전 18.2.1)에서 UTF-8 인코딩을 위한 지원을 추가합니다. SQL Server UTF-8 지원에 대한 자세한 내용은 다음을 참조하세요.
- [데이터 정렬 및 유니코드 지원](../../../relational-databases/collations/collation-and-unicode-support.md)
- [UTF-8 지원](#ctp23)

> [!IMPORTANT]
> Microsoft OLE DB Driver for SQL Server는 [GetACP](https://docs.microsoft.com/windows/win32/api/winnls/nf-winnls-getacp) 함수를 사용하여 DBTYPE_STR 입력 버퍼의 인코딩을 확인합니다. GetACP가 UTF-8 인코딩을 반환하는 시나리오는 지원되지 않습니다. 버퍼가 유니코드 데이터를 저장해야 하는 경우에는 버퍼 데이터 형식을 DBTYPE_WSTR(UTF-16으로 인코딩됨)로 설정해야 합니다.

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>UTF-8로 인코딩된 CHAR 또는 VARCHAR 열로의 데이터 삽입
삽입하기 위해 입력 매개 변수 버퍼를 만들 때 버퍼는 [DBBINDING 구조체](https://go.microsoft.com/fwlink/?linkid=2071182)의 배열을 사용하여 설명합니다. 각 DBBINDING 구조체는 단일 매개 변수를 소비자의 버퍼에 연결하고 데이터 값의 길이 및 형식과 같은 정보를 포함합니다. CHAR 형식의 입력 매개 변수 버퍼는 DBBINDING 구조체의 *wType*을 DBTYPE_STR로 설정해야 합니다. WCHAR 형식의 입력 매개 변수 버퍼는 DBBINDING 구조체의 *wType*을 DBTYPE_WSTR로 설정해야 합니다.

매개 변수를 사용하여 명령을 실행할 경우 드라이버에서 매개 변수 데이터 형식 정보를 생성합니다. 입력 버퍼 형식과 매개 변수 데이터 형식이 일치하면 드라이버에서 변환이 수행되지 않습니다. 그러지 않으면 드라이버에서 입력 매개 변수 버퍼를 매개 변수 데이터 형식으로 변환합니다. 매개 변수 데이터 형식은 사용자가 [ICommandWithParameters::SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577)를 호출하여 명시적으로 설정할 수 있습니다. 정보를 제공하지 않으면 드라이버는 (a) 문을 준비할 때 서버에서 열 메타데이터를 검색하거나 (b) 입력 매개 변수 데이터 형식에서 기본 변환을 시도하여 매개 변수 데이터 형식 정보를 파생합니다.

입력 버퍼 데이터 형식 및 매개 변수 데이터 형식에 따라 드라이버나 서버에 의해 입력 매개 변수 버퍼가 서버 열 데이터 정렬로 변환될 수 있습니다. 변환하는 동안 클라이언트 코드 페이지 또는 데이터베이스 데이터 정렬 코드 페이지에서 입력 버퍼의 모든 문자를 나타낼 수 없는 경우 데이터 손실이 발생할 수 있습니다. 다음 표에서는 UTF-8 사용 열에 데이터를 삽입할 때의 변환 프로세스를 설명합니다.

|버퍼 데이터 형식|매개 변수 데이터 형식|변환|사용자 예방 조치|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|클라이언트 코드 페이지에서 데이터베이스 데이터 정렬 코드 페이지로 서버 변환. 데이터베이스 데이터 정렬 코드 페이지에서 열 데이터 정렬 코드 페이지로 서버 변환|클라이언트 코드 페이지와 데이터베이스 데이터 정렬 코드 페이지에서 입력 데이터의 모든 문자를 표시할 수 있는지 확인합니다. 예를 들어 폴란드어 문자를 삽입하려면 클라이언트 코드 페이지를 1250(ANSI 중앙 유럽어)으로 설정할 수 있고 데이터베이스 데이터 정렬에서 폴란드어를 데이터 정렬 지정자(예: Polish_100_CI_AS_SC)로 사용할 수 있거나 UTF-8을 사용할 수 있어야 합니다.|
|DBTYPE_STR|DBTYPE_WSTR|클라이언트 코드 페이지에서 UTF-16 인코딩으로 드라이버 변환. UTF-16 인코딩에서 열 데이터 정렬 코드 페이지로 서버 변환|클라이언트 코드 페이지에서 입력 데이터의 모든 문자를 표시할 수 있는지 확인합니다. 예를 들어 폴란드어 문자를 삽입하려면 클라이언트 코드 페이지를 1250(ANSI 중앙 유럽어)로 설정할 수 있어야 합니다.|
|DBTYPE_WSTR|DBTYPE_STR|UTF-16 인코딩에서 데이터베이스 데이터 정렬 코드 페이지로 드라이버 변환. 데이터베이스 데이터 정렬 코드 페이지에서 열 데이터 정렬 코드 페이지로 서버 변환|데이터베이스 데이터 정렬 코드 페이지에서 입력 데이터의 모든 문자를 표시할 수 있는지 확인합니다. 예를 들어 폴란드어 문자를 삽입하려면 데이터베이스 데이터 정렬 코드 페이지에서 폴란드어를 데이터 정렬 지정자(예: Polish_100_CI_AS_SC)로 사용할 수 있거나 UTF-8을 사용할 수 있어야 합니다.|
|DBTYPE_WSTR|DBTYPE_WSTR|UTF-16에서 열 데이터 정렬 코드 페이지로 서버 변환|없음|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>UTF-8로 인코딩된 CHAR 또는 VARCHAR 열에서 데이터 검색
검색된 데이터를 위한 버퍼를 만들 때 버퍼는 [DBBINDING 구조체](https://go.microsoft.com/fwlink/?linkid=2071182)의 배열을 사용하여 설명합니다. 각 DBBINDING 구조는 검색된 행의 단일 열을 연결합니다. 열 데이터를 CHAR로 검색하려면 DBBINDING 구조체의 *wType*을 DBTYPE_STR로 설정합니다. 열 데이터를 WCHAR로 검색하려면 DBBINDING 구조체의 *wType*을 DBTYPE_WSTR로 설정합니다.

결과 버퍼 형식 표시기 DBTYPE_STR의 경우 드라이버는 UTF-8로 인코딩된 데이터를 클라이언트 인코딩으로 변환합니다. 사용자는 클라이언트 인코딩에서 UTF-8 열의 데이터를 표시할 수 있는지 확인해야 합니다. 표시할 수 없으면 데이터 손실이 발생할 수 있습니다.

결과 버퍼 형식 표시기 DBTYPE_WSTR의 경우 드라이버는 UTF-8로 인코딩된 데이터를 UTF-16 인코딩으로 변환합니다.

<a name="ctp23"></a>

### <a name="utf-8-support-sql-server-2019-ctp-23"></a>UTF-8 지원(SQL Server 2019 CTP 2.3)

[!INCLUDE[ss2019](../../../includes/sssqlv15-md.md)]에서는 가져오기 또는 내보내기 인코딩이나 텍스트 데이터의 데이터베이스 수준 또는 열 수준 데이터 정렬로 널리 사용되는 UTF-8 문자 인코딩이 완벽하게 지원됩니다. UTF-8은 `CHAR` 및 `VARCHAR` 데이터 형식에서 허용되며, `UTF8` 접미사를 사용하여 개체의 데이터 정렬을 만들거나 이 접미사를 갖는 데이터 정렬로 변경하여 설정합니다.

예를 들어 `LATIN1_GENERAL_100_CI_AS_SC`에서 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`로 변경합니다. UTF-8은 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에 제공된 보충 문자를 지원하는 Windows 데이터 정렬에서만 사용할 수 있습니다. `NCHAR` 및 `NVARCHAR`는 UTF-16 인코딩만 허용하며 변경되지 않고 유지됩니다.

이 기능은 사용 중인 문자 집합에 따라 스토리지 비용을 크게 절감하는 효과를 제공할 수 있습니다. 예를 들어 UTF-8 사용 데이터 정렬을 통해 ASCII(Latin) 문자열이 있는 기존 열 데이터 유형을 `NCHAR(10)`에서 `CHAR(10)`으로 변경하면 스토리지 요구 사항이 50% 감소합니다. 이러한 감소는 `NCHAR(10)`에는 스토리지로 20바이트가 필요하지만 `CHAR(10)`에는 동일한 유니코드 문자열에 대해 10바이트만 필요하기 때문입니다.

자세한 내용은 [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.

**CTP 2.1**[!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]설정 중 UTF-8 데이터 정렬을 기본값으로 선택하도록 지원을 추가했습니다.

**CTP 2.2** SQL Server 복제에서 UTF-8 문자 인코딩을 사용하도록 지원을 추가했습니다.

**CTP 2.3** BIN2 데이터 정렬(UTF8_BIN2)로 UTF-8 문자 인코딩을 사용하도록 지원을 추가했습니다.

## <a name="see-also"></a>참고 항목  
[SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[SQL Server용 OLE DB 드라이버에서 UTF-16 지원](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
