---
title: SQLManageDataSources | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f22fc952f0394f9e59ca8d67c76d0b00594b0759
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62466015"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**규칙**  
 도입 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLManageDataSources** 있는 사용자 수 설정, 추가 및 시스템 정보에 대 한 데이터 원본 삭제 대화 상자를 표시 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>인수  
 *hwnd*  
 [입력] 부모 창 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 **SQLManageDataSources** 경우에 FALSE를 반환 합니다 *hwnd* 유효한 창 핸들을 아닙니다. 그렇지 않으면 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLManageDataSources** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|에 대 한 호출 **ConfigDSN** 실패 했습니다.|  
|ODBC_ERROR_INVALID__HWND|잘못 된 창 핸들|합니다 *hwnd* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="managing-data-sources"></a>데이터 원본 관리  
 **SQLManageDataSources** 처음에 표시 합니다 **ODBC 데이터 원본 관리자** 대화 상자에서 다음 그림과에서 같이 합니다.  
  
 ![ODBC 데이터 원본 관리자 대화 상자](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 대화 상자에는 세 개의 탭에서 시스템 정보에 나열 된 데이터 소스 표시 됩니다. **사용자 DSN**하십시오 **시스템 DSN**, 및 **DSN 파일**합니다. 하는 경우 사용자 데이터 원본을 두 번 클릭 하거나 데이터 원본을 선택 하 고 클릭 **구성**하십시오 **SQLManageDataSources** 호출 **ConfigDSN** 설치는 ODBC_CONFIG_ 사용 하 여 DLL에서 DSN 옵션입니다.  
  
 클릭 하면 **추가**, **SQLManageDataSources** 표시를 **새 데이터 원본 만들기** 대화 상자에서 다음 그림에 표시 합니다.  
  
 ![새 데이터 소스 만들기 대화 상자](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 대화 상자에 설치 된 드라이버 목록이 표시 됩니다. 하는 경우 사용자는 드라이버를 두 번 클릭 또는 드라이버를 선택 하 고 클릭 **확인**를 **SQLManageDataSources** 호출 **ConfigDSN** 설치 DLL ODBC_ADD_DSN 옵션을 전달 합니다.  
  
 사용자는 데이터 원본을 선택 하 고 클릭 하는 경우 **제거할**, **SQLManageDataSources** 사용자가 데이터 원본을 삭제 하려는 지 여부를 묻습니다. 클릭 하면 **Yes**, **SQLManageDataSources** 호출 **ConfigDSN** 하려면 ODBC_REMOVE_DSN 옵션을 사용 하 여 설치 프로그램 DLL에서에서.  
  
 합니다 **새 데이터 원본 만들기** 대화 상자는 사용자 데이터 원본, 시스템 데이터 원본 또는 파일 데이터 원본 추가 또는 삭제 하는 데 사용 됩니다.  
  
## <a name="user-dsns"></a>사용자 Dsn  
 개별 사용자를 위해 만든 Dsn이 시스템 Dsn을 구별 하는 사용자 Dsn에 호출 됩니다. 사용자 Dsn 시스템 정보에 다음과 같이 등록 됩니다.  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>시스템 Dsn  
 합니다 **새 데이터 원본 만들기** 대화 상자를 사용 하면 로컬 컴퓨터 또는 삭제, 시스템 데이터 원본을 추가할 또는 시스템 데이터 원본에 대 한 구성을 설정 합니다.  
  
 시스템 데이터 원본 이름 (DSN)를 사용 하 여 설정 하는 데이터 원본이 동일한 컴퓨터에서 둘 이상의 사용자가 사용할 수 있습니다. 사용자가 컴퓨터에 로그온 하는 경우에 데이터 원본에 대 한 액세스를 얻을 수 있습니다를 시스템 전반에 걸쳐 서비스별 데도 수 있습니다.  
  
 시스템 DSN 시스템 정보 대신 HKEY_CURRENT_USER 항목 HKEY_LOCAL_MACHINE 항목에 등록 됩니다. 한 명의 사용자가 자신의 특정 사용자 이름 및 암호를 사용 하 여 로그온에 사용할 수 있지만 해당 컴퓨터의 모든 사용자가 또는 자동 시스템 전반에 걸쳐 서비스에 연결 되지 것입니다. 그러나 시스템 DSN가 하나의 컴퓨터에 연결 됩니다. 컴퓨터 간에 원격 Dsn을 사용 하 여 기능을 지원 하지는 않습니다. 시스템 Dsn 시스템 정보에 다음과 같이 등록 됩니다.  
  
 HKEY_LOCAL_MACHINE    SOFTWARE       ODBC          Odbc.ini  
  
## <a name="file-dsns"></a>파일 Dsn  
 파일 데이터 원본이 없습니다 데이터 원본 이름, 컴퓨터 데이터 원본에는 모든 사용자 또는 컴퓨터에 등록 되어 있지 않습니다. 해당 데이터 원본에 대 한 연결 정보는 모든 컴퓨터에 복사할 수 있는.dsn 파일에 포함 됩니다. 파일 데이터 원본 수를 공유할 수 있는.dsn 파일을 네트워크에 상주 하는 경우 있으며 동시에 사용할 수는 네트워크에서 여러 사용자가 사용자에 적절 한 드라이버를 설치 합니다. 파일 데이터 원본도 수 없습니다를 공유할 수 있는 경우에 단일 컴퓨터에만 사용할 수 있습니다.  
  
 파일 데이터 원본에 대 한 자세한 내용은 참조 하세요. [를 사용 하 여 파일 데이터 원본에 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)를 참조 하거나 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
## <a name="managing-drivers"></a>드라이버 관리  
 클릭할 경우 합니다 **드라이버** 탭에 **ODBC 데이터 원본 관리자** 대화 상자에서 **SQLManageDataSources** 시스템에 설치 된 ODBC 드라이버의 목록을 표시 드라이버에 대 한 정보를 제공 합니다. 다음 그림에 나와 있는 것 처럼 표시 되는 날짜는 드라이버의 생성 날짜.  
  
 ![ODBC 데이터 소스 관리자 드라이버 탭](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>추적 옵션  
 클릭할 경우 합니다 **추적** 탭에 **ODBC 데이터 원본 관리자** 대화 상자에서 **SQLManageDataSources** 다음에 표시 된 대로 추적 옵션을 표시 그림입니다.  
  
 ![ODBC 데이터 소스 관리자 추적 탭](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 클릭 하면 **추적 지금 시작** 을 클릭 한 다음 **확인**를 **SQLManageDataSources** 컴퓨터에서 현재 실행 중인 모든 응용 프로그램에 대해 수동으로 추적을 활성화 합니다.  
  
 사용자는 추적 파일의 이름을 지정 하는 경우는 **로그 파일 경로** 텍스트 상자 한 번의 클릭 만으로 **확인**를 **SQLManageDataSources** 설정는 **TraceFile** 지정된 된 이름에 시스템 정보 [ODBC] 섹션에는 키워드입니다.  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer에 대 한 지원 (Visual Studio Analyzer 이전 버전의 Visual Studio에만 포함 되었습니다.) Windows 8부터 제거 되었습니다. 문제 해결 메커니즘 대신 BID 추적을 사용 합니다.  
  
 사용자가 클릭 하면 **Visual Studio Analyzer 시작** 을 클릭 한 다음 **확인**, Visual Studio Analyzer 사용 하도록 설정 합니다. 될 때까지 설정 된 상태로 유지 됩니다 **Visual Studio Analyzer 중지** 를 클릭 합니다.  
  
 추적에 대 한 자세한 내용은 참조 하세요. [추적](../../../odbc/reference/develop-app/tracing.md)합니다. 에 대 한 자세한 내용은 합니다 **추적** 하 고 **TraceFile** 키워드를 참조 하세요 [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터 원본 만들기|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
