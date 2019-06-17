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
manager: craigg
ms.openlocfilehash: 8b432e8d40952574f1264e07a0b09e91a1e334b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537607"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 함수
**규칙**  
 도입 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLCreateDataSource** 사용자 데이터 소스를 추가할 수는 대화 상자를 표시 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>인수  
 *hwnd*  
 [입력] 부모 창 핸들입니다.  
  
 *lpszDS*  
 [입력] 데이터 원본 이름입니다. *lpszDS* null 포인터 이거나 빈 문자열이 될 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 **SQLCreateDataSource** 데이터 원본이 생성 되는 경우 TRUE를 반환 합니다. 그렇지 않으면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCreateDataSource** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|합니다 *hwnd* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_INVALID_DSN|잘못 된 DSN|합니다 *lpszDS* 인수 DSN에 대 한 잘못 된 문자열을 포함 합니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|에 대 한 호출 **ConfigDSN** ODBC_ADD_DSN 옵션을 사용 하 여 실패 했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 translator 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_USER_CANCELED|사용자가 취소 함 작업|사용자가 새 데이터 원본 만들기를 취소 했습니다.|  
|ODBC_ERROR_CREATE_DSN_FAILED|요청 된 DSN을 만들 수 없습니다.|데이터베이스에 연결할 수 없습니다. 에 대 한 호출 **SQLDriverConnect** 파일 DSN을 성공적으로 연결을 반환 하지 않았습니다.<br /><br /> 파일에 쓸 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 하는 경우 *hwnd* 가 null **SQLCreateDataSource** FALSE를 반환 합니다. 그렇지 않으면 표시는 **새 데이터 원본 만들기** 다음 그림에 나와 있는 것 처럼 데이터 원본 설정에서 유형을 선택 하는 것에 대 한 마법사 페이지를 사용 하 여 대화 상자.  
  
 ![새 데이터 소스 만들기 대화 상자: 유형 선택](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 기본 옵션은 **파일 데이터 원본**합니다. 데이터 원본을 선택한 경우 및 **다음** 클릭 하면 설치 된 드라이버의 목록을 포함 하는 다음 마법사 페이지가 표시 됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 드라이버 선택](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 경우 **취소할** 를 클릭 하면 대화 상자가 사라집니다 및 **SQLCreateDataSource** ODBC_ERROR_USER_CANCELED의 오류 코드를 사용 하 여 FALSE를 반환 합니다. 경우는 **사용자 데이터 원본** 또는 **시스템 데이터 원본** 옵션을 선택한 경우를 **고급** 단추는 사용할 수 없습니다.  
  
 경우는 **다음** 선택 된 원본 데이터의 유형에 따라, 단추는 다음 중 하나가 발생 합니다.  
  
-   하는 경우 **파일 데이터 원본** 를 선택 하면 마법사 페이지는 파일 이름을 입력 하 여 사용자에 대 한 표시 됩니다.  
  
-   경우 **사용자 데이터 원본** 또는 **시스템 데이터 원본** 를 선택 하면 검토를 위해 데이터 원본 유형과 드라이버를 표시 하는 마법사 페이지가 표시 됩니다 및 시기 **마침** 는 클릭 하면 데이터 원본 설정 됩니다.  
  
 하는 경우 **고급** 클릭할 드라이버 관련 정보를 입력 하 여 사용자에 대 한 새 데이터 원본 만들기 마법사 페이지에서 마법사 페이지가 표시 됩니다. 이 대화 상자의 텍스트 상자에서 다음 그림에 표시 된 대로 드라이버 및 반환 하 여 구분 된 키워드를 입력 합니다.  
  
 ![고급 파일 DSN 만들기 설정 대화 상자](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 추가 드라이버의 키워드에 대 한 설명을 찾을 수 있습니다 **SQLDriverConnect**합니다. 제외한 모든 **DSN** 허용 됩니다.  
  
 기본값은 **이 연결 확인** 옵션이 TRUE 인 합니다. 이 기본값은이 마법사 페이지가 활성화 여부에 적용 됩니다. 하는 경우 **확인** 를 클릭 하면 텍스트 상자에 지정 된 문자열 및 **이 연결 확인** 옵션 값이 캐시 됩니다. (경우는 **닫습니다** 단추 또는 **취소** 를 클릭 하면 새로 입력 한 모든 문자열을 텍스트 상자에 지정 되므로 드라이버 관련 정보가 손실 됩니다 및 **이 연결 확인** 옵션 값은 캐시 되지 않습니다.)  
  
 하는 경우 **파일 데이터 원본** 된 선택한 첫 번째 마법사 페이지에서 사용자 파일 이름을 입력 하도록 요청 드라이버를 선택한 후 고급 마법사 페이지에서 키워드 값이 입력 되었습니다. 클릭 **찾아보기** 검색할 파일 이름에 대 한 경우에서 기본 디렉터리는 **찾아보기** CommonFileDir HKEY_LOCAL_MACHINE\SOFTWARE\에 의해 지정 된 경로 결합 하 여 상자 지정 Microsoft\Windows\CurrentVersion 및 "ODBC\DataSources"입니다. (CommonFileDir "C:\Program Files\Common Files" 인 경우 기본 디렉터리 것 "C:\Program Files\Common Files\ODBC\Data Sources"입니다.)  
  
 파일 이름이 입력 된 경우 및 **다음** 클릭 하면 파일 이름을 입력 한 운영 체제의 표준 파일 명명 규칙에 대해 유효성을 검사 합니다. 파일 이름이 올바르지 않으면 오류 메시지 상자를 사용자에 게 알리는 파일 이름이 잘못 입력 된 합니다. 사용자 승인 메시지 상자를 후 포커스는 파일 이름을 입력 하는 마법사 페이지에 반환 됩니다. 파일 이름이 유효한 경우 다음 그림과에서 같이 선택한 키워드-값 쌍을 보여 주는 마법사 페이지, 검토를 위해 표시 됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 검토](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 경우 **완료** 클릭할 및 **파일 데이터 원본** 데이터 원본 유형으로 선택 된 경우에 **이 연결을 확인** 옵션을 TRUE로  **SQLDriverConnect** 를 호출 합니다 **SAVEFILE** 하 고 **드라이버** 키워드입니다. 합니다 *DriverCompletion* 인수를 SQL_DRIVER_COMPLETE로 설정 합니다. 파일 이름을 **SAVEFILE** 키워드는 입력 된 이름 또는 선택한 이름과 드라이버에 대 한 합니다 **드라이버** 키워드는 선택 된 이름입니다. 고급 마법사 페이지에서는 드라이버별 연결 문자열을 지정 하는 경우 해당 문자열은 후 추가 합니다 **드라이버** 키워드입니다.  
  
 하는 경우 **SQLDriverConnect** 드라이버 관리자와 관계 없이 SQL_SUCCESS를 반환 파일 DSN을 만들었습니다. **SQLCreateDataSource** TRUE를 반환 합니다. 하는 경우 **SQLDriverConnect** 경고 메시지와 관계 없이 SQL_SUCCESS를 반환 하지 않는 상자 나타냅니다 데이터 원본에 대 한 연결을 걸 수 없습니다. 최소 연결 정보를 사용 하 여 DSN은 여전히 만들 수 있습니다. 이 메시지 상자 취소 하거나 파일 DSN 만들기를 계속 진행 하는 사용자를 수 있습니다.  
  
 이 프로세스를 계속 하는 경우에 사용자 DSN 만들기를 계속 하기로, 처럼를 **이 연결을 확인** 옵션이 FALSE로 설정 되었습니다. FALSE가 반환 됩니다에 대 한 사용자를 취소 하기로 **SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED의 오류 코드입니다.  
  
 경우 **파일 데이터 원본** 데이터 원본 유형으로 선택 된 하며 **이 연결을 확인** 옵션은 FALSE, 파일 DSN을 사용 하 여 만들어집니다 합니다 **드라이버** 키워드 및 사용자 지정 연결 문자열 (있는 경우)에서 고급 마법사 페이지입니다. 파일 생성에 성공한 경우에 TRUE가 반환 됩니다 **SQLCreateDataSource**합니다. 파일 생성에 실패할 경우 오류 메시지 상자를 사용 하 여 모든 오류는 운영 체제에서 반환 된 사용자를 알립니다. 에 대 한 FALSE가 반환 **SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED의 오류 코드입니다. 파일 데이터 원본에 대 한 자세한 내용은 참조 하세요. [를 사용 하 여 파일 데이터 원본에 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)를 참조 하거나 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 하는 경우 **사용자** 하거나 **시스템 데이터 원본** 데이터 원본 유형으로 선택 된 **ConfigDSN** 드라이버 설치에 라이브러리를 ODBC_ADD_DSN를 사용 하 여 라고  *문제점과*합니다. 자세한 내용은 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터 원본 관리|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
