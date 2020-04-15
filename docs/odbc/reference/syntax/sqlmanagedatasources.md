---
title: SQLManage데이터소스 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b572a861af3479e1543be9fda9598cc7e25d36c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290221"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**규칙**  
 버전 출시: ODBC 2.0  
  
 **요약**  
 **SQLManageDataSource는** 사용자가 시스템 정보의 데이터 원본을 설정, 추가 및 삭제할 수 있는 대화 상자를 표시합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>인수  
 *Hwnd*  
 [입력] 부모 창 핸들입니다.  
  
## <a name="returns"></a>반환  
 **SQLManageDataSource** *hwnd* 유효한 창 핸들 되지 않은 경우 FALSE를 반환 합니다. 그러지 않으면 TRUE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLManageDataSource** FALSE를 반환하는 경우 **SQLInstallerError**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|**ConfigDSN에** 대한 호출이 실패했습니다.|  
|ODBC_ERROR_INVALID__HWND|창 핸들이 잘못되었습니다.|*hwnd* 인수가 유효하지 않거나 NULL입니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="managing-data-sources"></a>데이터 원본 관리  
 **SQLManageDataSource는** 처음에 다음 그림과 같이 **ODBC 데이터 원본 관리자** 대화 상자가 표시됩니다.  
  
 ![ODBC 데이터 소스 관리자 대화 상자](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 대화 상자에는 시스템 정보에 나열된 데이터 원본이 사용자 **DSN,** **시스템 DSN**및 **파일 DSN의**세 가지 탭 아래에 표시됩니다. 사용자가 데이터 원본을 두 번 클릭하거나 데이터 원본을 선택하고 **구성을**클릭하면 **SQLManageDataSource는** ODBC_CONFIG_DSN 옵션을 사용하여 설정 DLL에서 **ConfigDSN을** 호출합니다.  
  
 사용자가 **추가를**클릭하면 **SQLManageDataSource는** 다음 그림에 표시된 **새 데이터 원본 만들기** 대화 상자가 표시됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 대화 상자에 설치된 드라이버 목록이 표시됩니다. 사용자가 드라이버를 두 번 클릭하거나 드라이버를 선택하고 **확인을**클릭하면 **SQLManageDataSource는** 설정 DLL에서 **ConfigDSN을** 호출하고 ODBC_ADD_DSN 옵션을 전달합니다.  
  
 사용자가 데이터 원본을 선택하고 **제거를**클릭하면 **SQLManageDataSource는** 사용자가 데이터 원본을 삭제할지 여부를 묻습니다. 사용자가 **예**, **SQLManageDataSource를** 클릭하면 ODBC_REMOVE_DSN 옵션을 사용하여 설정 DLL에서 **ConfigDSN을** 호출합니다.  
  
 **새 데이터 원본 만들기** 대화 상자는 사용자 데이터 원본, 시스템 데이터 원본 또는 파일 데이터 원본을 추가하거나 삭제하는 데 사용됩니다.  
  
## <a name="user-dsns"></a>사용자 DSN  
 개별 사용자를 위해 만든 DSN을 시스템 DSN과 구분하기 위해 사용자 DSN이라고 합니다. 사용자 DSN은 시스템 정보에 다음과 같이 등록됩니다.  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>시스템 DSN  
 **새 데이터 원본 만들기** 대화 상자를 사용하면 로컬 컴퓨터에 시스템 데이터 원본을 추가하거나 삭제하거나 시스템 데이터 원본에 대한 구성을 설정할 수 있습니다.  
  
 시스템 데이터 원본 이름(DSN)으로 설정된 데이터 원본은 동일한 컴퓨터에서 두 명 이상의 사용자가 사용할 수 있습니다. 또한 시스템 전체 서비스에서 사용할 수 있으며, 컴퓨터에 로그온한 사용자가 없는 경우에도 데이터 원본에 액세스할 수 있습니다.  
  
 시스템 DSN은 HKEY_CURRENT_USER 항목이 아닌 시스템 정보의 HKEY_LOCAL_MACHINE 항목에 등록됩니다. 특정 사용자 이름과 암호로 로그온하는 한 사용자에 연결되지 는 않지만 해당 컴퓨터의 모든 사용자 또는 자동 시스템 전체 서비스에서 사용할 수 있습니다. 그러나 시스템 DSN은 하나의 컴퓨터에 연결되어 있습니다. 컴퓨터 간에 원격 DSN을 사용하는 기능은 지원하지 않습니다. 시스템 DSN은 시스템 정보에 다음과 같이 등록됩니다.  
  
 HKEY_LOCAL_MACHINE 소프트웨어 ODBC Odbc.ini  
  
## <a name="file-dsns"></a>파일 DSN  
 파일 데이터 원본에는 컴퓨터 데이터 원본과 마찬가지로 데이터 원본 이름이 없으며 한 사용자 나 컴퓨터에 등록되지 않습니다. 해당 데이터 원본에 대한 연결 정보는 모든 컴퓨터에 복사할 수 있는 .dsn 파일에 포함되어 있습니다. 파일 데이터 원본을 공유할 수 있으며, 이 경우 .dsn 파일은 네트워크에 상주하며 사용자가 적절한 드라이버를 설치하는 한 네트워크의 여러 사용자가 동시에 사용할 수 있습니다. 파일 데이터 원본은 공유할 수 없는 경우 단일 컴퓨터에서만 사용할 수 있습니다.  
  
 파일 데이터 원본에 대한 자세한 내용은 [파일 데이터 원본 을 사용하여 연결을](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)참조하거나 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)를 참조하십시오.  
  
## <a name="managing-drivers"></a>드라이버 관리  
 사용자가 **ODBC 데이터 원본 관리자** 대화 상자에서 **드라이버** 탭을 클릭하면 **SQLManageDataSource는** 시스템에 설치된 ODBC 드라이버 목록과 드라이버에 대한 정보를 표시합니다. 표시된 날짜는 다음 그림과 같이 드라이버 생성 날짜입니다.  
  
 ![ODBC 데이터 소스 관리자 드라이버 탭](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>추적 옵션  
 사용자가 **ODBC 데이터 원본 관리자** 대화 상자에서 **추적** 탭을 클릭하면 다음 그림과 같이 **SQLManageDataSource가** 추적 옵션을 표시합니다.  
  
 ![ODBC 데이터 소스 관리자 추적 탭](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 사용자가 **지금 추적 시작을** 클릭한 다음 **확인을**클릭하면 **SQLManageDataSource를** 사용하여 컴퓨터에서 현재 실행 중인 모든 응용 프로그램에 대해 수동으로 추적할 수 있습니다.  
  
 사용자가 **로그 파일 경로** 텍스트 상자에서 추적 파일의 이름을 지정한 다음 **확인을**클릭하면 **SQLManageDataSource는** 시스템 정보의 [ODBC] 섹션에서 **TraceFile** 키워드를 지정된 이름으로 설정합니다.  
  
> [!IMPORTANT]  
>  비주얼 스튜디오 분석기지원은 Windows 8부터 제거되었습니다(Visual Studio 분석기는 이전 버전의 Visual Studio에만 포함되었습니다.) 대체 문제 해결 메커니즘을 보려면 BID 추적을 사용합니다.  
  
 사용자가 **시각적 스튜디오 분석기 시작을** 클릭한 다음 **확인을**클릭하면 Visual Studio 분석기가 활성화됩니다. **비주얼 스튜디오 분석기 중지를** 클릭할 때까지 활성화된 상태로 유지됩니다.  
  
 추적에 대한 자세한 내용은 [추적](../../../odbc/reference/develop-app/tracing.md)을 참조하십시오. **추적** 및 **추적 파일** 키워드에 대한 자세한 내용은 [ODBC 하위 키를](../../../odbc/reference/install/odbc-subkey.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본 만들기|[SQLCreate데이터 소스](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
