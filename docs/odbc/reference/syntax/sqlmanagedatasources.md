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
ms.openlocfilehash: 819856a584c6133e28e222a704b720337f99cd9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018957"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**규칙**  
 소개 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLManageDataSources** 사용자가 시스템 정보에서 데이터 원본을 설정, 추가 및 삭제할 수 있는 대화 상자를 표시 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>인수  
 *hwnd*  
 입력 부모 창 핸들입니다.  
  
## <a name="returns"></a>반환  
 *Hwnd* 가 유효한 창 핸들이 아니면 **SQLManageDataSources** 는 FALSE를 반환 합니다. 그러지 않으면 TRUE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLManageDataSources** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|**ConfigDSN** 에 대 한 호출이 실패 했습니다.|  
|ODBC_ERROR_INVALID__HWND|창 핸들이 잘못 되었습니다.|*Hwnd* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="managing-data-sources"></a>데이터 원본 관리  
 **SQLManageDataSources** 는 다음 그림에 표시 된 것 처럼 처음에 **ODBC 데이터 원본 관리자** 대화 상자를 표시 합니다.  
  
 ![ODBC 데이터 소스 관리자 대화 상자](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 대화 상자에는 **사용자 DSN**, **시스템 DSN**및 **파일 dsn**의 세 탭에서 시스템 정보에 나열 된 데이터 원본이 표시 됩니다. 사용자가 데이터 원본을 두 번 클릭 하거나 데이터 원본을 선택 하 고 **구성**을 클릭 하면 **SQLManageDataSources** 는 ODBC_CONFIG_DSN 옵션을 사용 하 여 설치 DLL에서 **ConfigDSN** 을 호출 합니다.  
  
 사용자가 **추가**를 클릭 하면 다음 그림과 같이 **새 데이터 원본 만들기** 대화 상자가 표시 됩니다 **SQLManageDataSources** .  
  
 ![새 데이터 소스 만들기 대화 상자](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 이 대화 상자에는 설치 된 드라이버의 목록이 표시 됩니다. 사용자가 드라이버를 두 번 클릭 하거나 드라이버를 선택 하 고 **확인**을 클릭 하면 **SQLMANAGEDATASOURCES** 가 설치 DLL에서 **ConfigDSN** 을 호출 하 여 ODBC_ADD_DSN 옵션으로 전달 합니다.  
  
 사용자가 데이터 원본을 선택 하 고 **제거**를 클릭 하면 **SQLManageDataSources** 는 사용자가 데이터 원본을 삭제할지 여부를 묻는 메시지를 표시 합니다. 사용자가 **예**를 클릭 하면 **SQLManageDataSources** 는 ODBC_REMOVE_DSN 옵션을 사용 하 여 설치 DLL에서 **ConfigDSN** 을 호출 합니다.  
  
 **새 데이터 원본 만들기** 대화 상자는 사용자 데이터 원본, 시스템 데이터 원본 또는 파일 데이터 원본을 추가 하거나 삭제 하는 데 사용 됩니다.  
  
## <a name="user-dsns"></a>사용자 Dsn  
 개별 사용자를 위해 만든 Dsn은 시스템 Dsn과 구분 하기 위해 사용자 Dsn 이라고 합니다. 사용자 Dsn은 다음과 같이 시스템 정보에 등록 됩니다.  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>시스템 Dsn  
 **새 데이터 원본 만들기** 대화 상자를 사용 하 여 로컬 컴퓨터에 시스템 데이터 원본을 추가 하거나 하나를 삭제 하거나 시스템 데이터 원본에 대 한 구성을 설정할 수 있습니다.  
  
 시스템 DSN (데이터 원본 이름)을 사용 하 여 설정 된 데이터 원본을 동일한 컴퓨터의 여러 사용자가 사용할 수 있습니다. 또한 시스템에 로그온 한 사용자가 없는 경우에도 데이터 원본에 대 한 액세스 권한을 얻을 수 있는 시스템 시스템 서비스에서 사용할 수 있습니다.  
  
 시스템 DSN이 HKEY_CURRENT_USER 항목이 아닌 시스템 정보의 HKEY_LOCAL_MACHINE 항목에 등록 되어 있습니다. 특정 사용자 이름 및 암호를 사용 하 여 로그온 하는 한 사용자에 게는 연결 되지 않지만, 해당 컴퓨터의 모든 사용자 또는 자동 전체 시스템 서비스에서 사용할 수 있습니다. 그러나 시스템 DSN은 한 대의 컴퓨터에 연결 되어 있습니다. 컴퓨터 간 원격 Dsn을 사용 하는 기능을 지원 하지 않습니다. 시스템 Dsn은 다음과 같이 시스템 정보에 등록 됩니다.  
  
 HKEY_LOCAL_MACHINE SOFTWARE ODBC setup.ini  
  
## <a name="file-dsns"></a>파일 Dsn  
 파일 데이터 원본에는 컴퓨터 데이터 원본 처럼 데이터 원본 이름이 없고 한 사용자 또는 컴퓨터에 등록 되지 않습니다. 해당 데이터 원본에 대 한 연결 정보는 컴퓨터로 복사 될 수 있는 dsn 파일에 포함 되어 있습니다. 파일 데이터 원본을 공유할 수 있으며,이 경우 dsn 파일은 네트워크에 상주 하며, 사용자에 게 적절 한 드라이버가 설치 되어 있으면 네트워크의 여러 사용자가 동시에 사용할 수 있습니다. 파일 데이터 원본도 unshareable 수 있으며,이 경우 단일 컴퓨터 에서만 사용할 수 있습니다.  
  
 파일 데이터 원본에 대 한 자세한 내용은 [파일 데이터 원본을 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)를 참조 하세요.  
  
## <a name="managing-drivers"></a>드라이버 관리  
 사용자가 **Odbc 데이터 원본 관리자** 대화 상자에서 **드라이버** 탭을 클릭 하면 **SQLManageDataSources** 는 시스템에 설치 된 odbc 드라이버 목록과 드라이버에 대 한 정보를 표시 합니다. 표시 되는 날짜는 다음 그림과 같이 드라이버를 만든 날짜입니다.  
  
 ![ODBC 데이터 소스 관리자 드라이버 탭](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>추적 옵션  
 사용자가 **ODBC 데이터 원본 관리자** 대화 상자의 **추적** 탭을 클릭 하면 다음 그림과 같이 **SQLManageDataSources** 에서 추적 옵션을 표시 합니다.  
  
 ![ODBC 데이터 소스 관리자 추적 탭](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 사용자가 **지금 추적 시작** 을 클릭 한 다음 **확인**을 클릭 하면 **SQLManageDataSources** 는 컴퓨터에서 현재 실행 중인 모든 응용 프로그램에 대해 수동으로 추적을 사용 하도록 설정 합니다.  
  
 사용자가 **로그 파일 경로** 텍스트 상자에 추적 파일의 이름을 지정 하 고 **확인**을 클릭 하면 **SQLMANAGEDATASOURCES** 는 시스템 정보의 [ODBC] 섹션에서 **tracefile** 키워드를 지정 된 이름으로 설정 합니다.  
  
> [!IMPORTANT]  
>  Visual Studio 분석기에 대 한 지원은 Windows 8부터 제거 되었습니다 (Visual Studio 분석기 이전 버전의 Visual Studio에만 포함 됨). 다른 문제 해결 메커니즘을 사용 하려면 입찰 추적을 사용 합니다.  
  
 사용자가 **시작 Visual Studio 분석기** 를 클릭 한 다음 **확인**을 클릭 하면 Visual Studio 분석기 사용 됩니다. **중지 Visual Studio 분석기** 을 클릭할 때까지 활성화 된 상태로 유지 됩니다.  
  
 추적에 대 한 자세한 내용은 [추적](../../../odbc/reference/develop-app/tracing.md)을 참조 하세요. **Trace** 및 **tracefile** 키워드에 대 한 자세한 내용은 [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)를 참조 하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 소스 만들기|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
