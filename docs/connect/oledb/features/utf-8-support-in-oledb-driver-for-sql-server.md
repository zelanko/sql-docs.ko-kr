---
title: SQL Server용 OLE DB 드라이버에서 UTF-8 지원| Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 UTF-8 지원
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: f410ddf4e3843936da6f93f488f379feea863e59
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744857"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에서 UTF-8 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB Driver for SQL Server (버전 18.2.1) 인코딩을 u t F-8 서버에 대 한 지원을 추가합니다. SQL Server u t F-8 지원에 대 한 자세한 내용은 다음을 참조 합니다.
- [데이터 정렬 및 유니코드 지원](../../../relational-databases/collations/collation-and-unicode-support.md)
- [UTF-8 지원(CTP 2.2)](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-22)

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>데이터 삽입을 u t F-8로 인코드된 CHAR 또는 VARCHAR 열
버퍼의 배열을 사용 하 여 설명 삽입에 대 한 입력된 매개 변수 버퍼를 만들면 [DBBINDING 구조체](https://go.microsoft.com/fwlink/?linkid=2071182)합니다. DBBINDING 구조의 각 소비자의 버퍼에 단일 매개 변수를 연결 하 고 같은 길이 데이터 값의 형식 정보를 포함 합니다. CHAR 형식의 입력된 매개 변수 버퍼를 *wType* DBBINDING의 DBTYPE_STR로 구조를 설정 합니다. WCHAR 형식의 입력된 매개 변수 버퍼를 *wType* 의 DBBINDING 구조 DBTYPE_WSTR로 설정 해야 합니다.

매개 변수를 사용 하 여 명령을 실행 하는 경우 드라이버는 매개 변수 데이터 형식 정보를 생성 합니다. 입력된 버퍼 형식 및 매개 변수 데이터 형식 일치 하는 경우 드라이버에서 변환이 수행 됩니다. 그렇지 않으면 드라이버 매개 변수 데이터 형식으로 입력된 매개 변수 버퍼를 변환합니다. 매개 변수 데이터 형식을 호출 하 여 명시적으로 사용자가 설정할 수 있습니다 [icommandwithparameters:: Setparameterinfo](https://go.microsoft.com/fwlink/?linkid=2071577)합니다. 정보 제공 되지 않는 경우 드라이버 (를) 열 메타 데이터 검색 서버에서 문 준비 될 때 또는 (b) 입력된 매개 변수 데이터 형식에서 기본 변환을 시도 하 여 매개 변수 데이터 형식 정보를 파생 합니다.

입력된 매개 변수 버퍼 드라이버에 의해 또는 입력된 버퍼 데이터 형식 및 매개 변수 데이터 형식에 따라 서버에서 서버 열 데이터 정렬으로 변환 될 수 있습니다. 변환 시 클라이언트 코드 페이지 또는 데이터베이스 데이터 정렬 코드 페이지는 입력된 버퍼의 모든 문자를 나타낼 수 없는 경우 데이터 손실이 발생할 수 있습니다. 다음 표에서 열을 사용 하도록 설정를 u t F-8로 데이터를 삽입 하는 경우 변환 프로세스를 설명 합니다.

|버퍼 데이터 형식|매개 변수 데이터 형식|변환|사용자 예방 조치|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|데이터베이스 데이터 정렬 코드 페이지를 클라이언트 코드 페이지에서 서버 변환 데이터베이스 데이터 정렬 코드 페이지에서 열 데이터 정렬 코드 페이지 변환을 서버입니다.|클라이언트 코드 페이지와 데이터베이스 데이터 정렬 코드 페이지는 입력된 데이터의 모든 문자를 나타낼 수 있는지 확인 합니다. 예를 들어, 폴란드어 문자를 삽입 하려면 클라이언트 코드 페이지 1250 (ANSI 중앙 유럽)로 설정 수 및 데이터베이스 데이터 정렬은 데이터 정렬 지정자 (예를 들어 Polish_100_CI_AS_SC)으로 폴란드어를 사용 하거나 u t F-8이 사용 하도록 설정 합니다.|
|DBTYPE_STR|DBTYPE_WSTR|드라이버에서로의 변환이 클라이언트 코드 페이지 인코딩을 u t F-16 열 데이터 정렬 코드 페이지 인코딩을 u t F-16에서 server 변환입니다.|클라이언트 코드 페이지에서 입력된 데이터의 모든 문자를 나타낼 수 있는지 확인 합니다. 예를 들어, 폴란드어 문자를 삽입 하려면 클라이언트 코드 페이지 1250 (ANSI 중앙 유럽어)로 설정할 수 없습니다.|
|DBTYPE_WSTR|DBTYPE_STR|데이터베이스 데이터 정렬 코드 페이지 인코딩을 u t F-16에서 드라이버 변환 데이터베이스 데이터 정렬 코드 페이지에서 열 데이터 정렬 코드 페이지 변환을 서버입니다.|데이터베이스 데이터 정렬 코드 페이지에서 입력된 데이터의 모든 문자를 나타낼 수 있는지 확인 합니다. 예를 들어, 폴란드어 문자를 삽입 하려면 데이터베이스 데이터 정렬 코드 페이지 폴란드어 데이터 정렬 지정자 (예를 들어 Polish_100_CI_AS_SC)으로 사용할 수 있습니다 또는 u t F-8이 사용 하도록 설정 합니다.|
|DBTYPE_WSTR|DBTYPE_WSTR|열 데이터 정렬 코드 페이지 u t F-16 server 변환 합니다.|없음|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>데이터 검색을 u t F-8에서 인코딩 CHAR 또는 VARCHAR 열
버퍼의 배열을 사용 하 여 설명 되어 검색된 된 데이터에 대 한 버퍼를 만들 때 [DBBINDING 구조체](https://go.microsoft.com/fwlink/?linkid=2071182)합니다. DBBINDING 구조의 각 검색된 행의 단일 열에 연결합니다. CHAR로 열 데이터를 검색 하려면 다음을 설정 합니다 *wType* DBTYPE_STR DBBINDING 구조의 합니다. WCHAR로 열 데이터를 검색 하려면 다음을 설정 합니다 *wType* DBTYPE_WSTR DBBINDING 구조의 합니다.

드라이버 결과 버퍼 유형 표시기 DBTYPE_STR에 대 한 인코딩이 u t F-8로 인코딩된 데이터를 변환 합니다. 사용자 확인 해야 인코딩 클라이언트를 나타낼 수 있습니다 데이터가 고, 그렇지 u t F-8 열에서 데이터 손실이 발생할 수 있습니다.

결과 버퍼 형식 표시기 DBTYPE_WSTR에 대 한 드라이버는 utf-16 인코딩을 u t F-8로 인코딩된 데이터를 변환합니다.
  
## <a name="see-also"></a>참고 항목  
[SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[SQL Server용 OLE DB 드라이버에서 UTF-16 지원](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
