---
title: SQLManageDataSources | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8785fef25830aa3987470a8007e115da1cc73a42
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**규칙**  
 ODBC 2.0 도입 된 버전:  
  
 **요약**  
 **SQLManageDataSources** 된 사용자 수를 설정, 추가 및 시스템 정보에 대 한 데이터 원본을 삭제 대화 상자를 표시 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>인수  
 *hwnd*  
 [입력] 부모 창 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 **SQLManageDataSources** 경우 FALSE를 반환 합니다. *hwnd* 은 유효한 창 핸들이 아닙니다. 그렇지 않으면 TRUE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLManageDataSources** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|에 대 한 호출 **ConfigDSN** 실패 했습니다.|  
|ODBC_ERROR_INVALID__HWND|잘못 된 창 핸들|*hwnd* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="managing-data-sources"></a>데이터 소스 관리  
 **SQLManageDataSources** 처음에 표시 됩니다는 **ODBC 데이터 원본 관리자** 대화 상자에서 다음 그림에 나와 있는 것 처럼 합니다.  
  
 ![ODBC 데이터 원본 관리자 대화 상자](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 시스템 정보 세 개의 탭 아래에 나열 된 데이터 소스를 표시 하는 대화 상자: **사용자 DSN**, **시스템 DSN**, 및 **파일 DSN**합니다. 하는 경우 사용자가 데이터 원본을 두 번 클릭 하거나 데이터 원본을 선택 하 고 클릭 **구성**, **SQLManageDataSources** 호출 **ConfigDSN** 설치는 ODBC_CONFIG_ 하 여 DLL에서 DSN 옵션입니다.  
  
 사용자가 클릭할 경우 **추가**, **SQLManageDataSources** 표시는 **새 데이터 원본 만들기** 대화 상자에서 다음 그림에 나와 있습니다.  
  
 ![새 데이터 소스 만들기 대화 상자](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 대화 상자에 설치 된 드라이버 목록이 표시 됩니다. 하는 경우 사용자가 드라이버를 두 번 클릭 하거나 드라이버를 선택 하 고 클릭 **확인**, **SQLManageDataSources** 호출 **ConfigDSN** DLL 설치 프로그램에서 ODBC_ADD_DSN 옵션을 전달 합니다.  
  
 사용자가 데이터 소스를 선택한를 클릭할 경우 **제거**, **SQLManageDataSources** 데이터 원본을 삭제 하려면 사용자가 있는지 여부를 묻습니다. 사용자가 클릭할 경우 **예**, **SQLManageDataSources** 호출 **ConfigDSN** DLL 하려면 ODBC_REMOVE_DSN 옵션으로 설정에서 합니다.  
  
 **새 데이터 원본 만들기** 대화 상자는 추가 또는 사용자 데이터 원본, 시스템 데이터 원본 또는 파일 데이터 원본을 삭제 하는 데 사용 됩니다.  
  
## <a name="user-dsns"></a>사용자 Dsn  
 개별 사용자에 대해 생성 하는 Dsn 시스템 Dsn을 구별 하는 사용자 Dsn에 호출 됩니다. 다음과 같이 시스템 정보에 사용자 Dsn은 등록 합니다.  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>시스템 Dsn  
 **새 데이터 원본 만들기** 대화 상자에서는 로컬 컴퓨터 또는 하나를 삭제 하는 시스템 데이터 원본을 추가 하려면 또는 시스템 데이터 원본에 대 한 구성을 설정할 수 있습니다.  
  
 시스템 데이터 원본 이름 (DSN)를 사용 하 여 설정 하는 데이터 소스는 같은 컴퓨터에서 둘 이상의 사용자가 사용할 수 있습니다. 또한 시스템 전체 서비스에 액세스할 수 있게 데이터 원본에 없는 사용자가 컴퓨터에 로그온 하는 경우에 사용할 수 있습니다.  
  
 시스템 DSN 시스템 정보 아닌 HKEY_CURRENT_USER 항목은 HKEY_LOCAL_MACHINE 항목에 등록 됩니다. 한 명의 사용자가 자신의 특정 사용자 이름 및 암호를 사용 하 여 로그온 하지만 사용할 수 있는 자동 시스템 전체 서비스에서 또는 해당 컴퓨터의 모든 사용자가을 따르지 않으므로 합니다. 그러나 시스템 DSN, 한 컴퓨터에 연결 됩니다. 컴퓨터 간의 원격 Dsn을 사용 하 여 기능을 지원 하지 않습니다. 시스템 정보에 다음과 같은 시스템 Dsn은 등록 합니다.  
  
 HKEY_LOCAL_MACHINE 소프트웨어 ODBC Odbc.ini  
  
## <a name="file-dsns"></a>파일 Dsn  
 파일 데이터 원본이 없는 데이터 원본 이름 처럼 컴퓨터 데이터 소스를 수행 하 고 하나의 사용자 또는 컴퓨터에 등록 되어 있지 않습니다. 해당 데이터 원본에 대 한 연결 정보는 모든 컴퓨터에 복사할 수 있는.dsn 파일에 포함 됩니다. 파일 데이터 원본을 수 공유 가능,.dsn 파일을 네트워크에 상주 하는 경우 있으며 동시에 사용할 수는 네트워크에서 여러 사용자가 사용자가 적절 한 드라이버를 설치 합니다. 파일 데이터 원본도 수 있습니다 공유할 수 있는,이 경우 단일 컴퓨터에만 사용할 수 있습니다.  
  
 파일 데이터 원본에 대 한 자세한 내용은 참조 하십시오. [를 사용 하 여 파일 데이터 원본 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), 참조 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
## <a name="managing-drivers"></a>드라이버 관리  
 사용자가 클릭할 경우의 **드라이버** 탭에 **ODBC 데이터 원본 관리자** 대화 상자, **SQLManageDataSources** 시스템에 설치 된 ODBC 드라이버의 목록이 표시 됩니다 드라이버에 대 한 정보를 제공 합니다. 다음 그림에 나와 있는 것 처럼 드라이버의 만든 날짜를가 하는 표시 되는 날짜입니다.  
  
 ![ODBC 데이터 소스 관리자 드라이버 탭](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>추적 옵션  
 사용자가 클릭할 경우의 **추적** 탭에 **ODBC 데이터 원본 관리자** 대화 상자, **SQLManageDataSources** 다음에 표시 된 것 처럼 추적 옵션을 표시 그림입니다.  
  
 ![ODBC 데이터 소스 관리자 추적 탭](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 사용자가 클릭할 경우 **추적 지금 시작** 클릭 한 다음 클릭 **확인**, **SQLManageDataSources** 컴퓨터에서 현재 실행 중인 모든 응용 프로그램에 대해 수동으로 추적할 수 있습니다.  
  
 사용자는 추적 파일의 이름을 지정 하는 경우는 **로그 파일 경로** 텍스트 상자에 한 번의 클릭 한 다음 **확인**, **SQLManageDataSources** 설정의 **TraceFile** 지정된 된 이름에 시스템 정보 [ODBC] 섹션에는 키워드입니다.  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer에 대 한 지원 (Visual Studio Analyzer 이전 버전의 Visual Studio에만 포함 되었습니다.) Windows 8 부터는 제거 되었습니다. 다른 방법은 문제 해결 메커니즘 BID 추적을 사용 합니다.  
  
 사용자가 클릭할 경우 **Visual Studio Analyzer 시작** 클릭 한 다음 클릭 **확인**, Visual Studio Analyzer를 사용할 수 있습니다. 될 때까지 사용 하도록 설정 되어 **Visual Studio Analyzer 중지** 를 클릭 합니다.  
  
 추적에 대 한 자세한 내용은 참조 하십시오. [추적](../../../odbc/reference/develop-app/tracing.md)합니다. 에 대 한 자세한 내용은 **추적** 및 **TraceFile** 키워드 참조 [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터 소스 만들기|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|

