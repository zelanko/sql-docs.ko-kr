---
title: SQLCreateDataSource 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 87a5383d5580c9c6ca706e13e1fd3171713511bf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 함수
**규칙**  
 ODBC 2.0 도입 된 버전:  
  
 **요약**  
 **SQLCreateDataSource** 사용자 데이터 원본을 추가할 수 있는 대화 상자가 표시 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 **SQLCreateDataSource** 데이터 원본이 생성 된 경우 TRUE를 반환 합니다. 그렇지 않으면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLCreateDataSource** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|*hwnd* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_INVALID_DSN|잘못 된 DSN|*lpszDS* 인수에는 DSN에 대 한 잘못 된 문자열이 포함 되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|에 대 한 호출 **ConfigDSN** ODBC_ADD_DSN 옵션과 함께 실패 했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 변환기 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_USER_CANCELED|사용자가 취소 작업|사용자는 새 데이터 원본 작성을 취소 했습니다.|  
|ODBC_ERROR_CREATE_DSN_FAILED|요청 된 DSN을 만들 수 없습니다.|데이터베이스;에 연결할 수 없습니다. 에 대 한 호출 **SQLDriverConnect** 파일 DSN 성공적으로 연결을 반환 하지 않았습니다.<br /><br /> 파일에 쓸 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 경우 *hwnd* 매개 변수가 null 이면 **SQLCreateDataSource** FALSE를 반환 합니다. 그렇지 않으면 표시는 **새 데이터 원본 만들기** 다음 그림에 나와 있는 것 처럼를 설정 해야 데이터 소스의 형식을 선택 하기 위한 마법사 페이지와 대화 상자.  
  
 ![새 데이터 소스 만들기 대화 상자: 유형 선택](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 기본 옵션은 **파일 데이터 원본**합니다. 데이터 원본을 선택한 경우 및 **다음** 클릭 하면 설치 된 드라이버의 목록이 포함 된 다음 마법사 페이지가 표시 됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 드라이버 선택](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 경우 **취소** 를 클릭 하면 대화 상자가 사라집니다 및 **SQLCreateDataSource** ODBC_ERROR_USER_CANCELED의 오류 코드와 FALSE를 반환 합니다. 경우는 **사용자 데이터 원본이** 또는 **시스템 데이터 원본** 옵션을 선택한는 **고급** 단추는 사용할 수 없습니다.  
  
 경우는 **다음** 원본을 선택 된 데이터의 유형에 따라, 단추를 클릭 하면 다음 중 하나가 발생 합니다.  
  
-   경우 **파일 데이터 소스** 를 선택 하면 사용자가 파일 이름을 입력 하는 마법사 페이지가 표시 됩니다.  
  
-   경우 **사용자 데이터 원본** 또는 **시스템 데이터 원본** 를 선택 하면 데이터 원본 유형과 드라이버를 표시 하는 마법사 페이지 검토를 위해 표시 되 및 시기 **마침** 은 클릭 하면 데이터 원본 설정 되어 있습니다.  
  
 경우 **고급** 클릭할 드라이버 관련 정보를 입력 하 고 사용자에 대 한 새 데이터 원본 만들기 마법사 페이지에서 마법사 페이지가 표시 됩니다. 이 대화 상자의 텍스트 상자에 다음 그림에 표시 된 대로 드라이버와 구분 하 여 반환 되 면 키워드를 입력 합니다.  
  
 ![파일 DSN 만들기 설정 대화 상자 고급](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 추가 드라이버 관련 키워드에 대 한 설명을 확인할 수 있습니다 **SQLDriverConnect**합니다. 제외 하 고 모두 **DSN** 허용 됩니다.  
  
 에 대 한 기본값은 **이 연결 확인** 옵션은 TRUE입니다. 이 기본값은이 마법사 페이지가 활성화 여부에 적용 됩니다. 경우 **확인** 를 클릭 하면 텍스트 상자에 지정 된 문자열 및 **이 연결 확인** 옵션 값이 캐시 됩니다. (하는 경우는 **닫기** 단추 또는 **취소** 를 클릭 하면 새로 입력 한 모든 문자열 텍스트 상자에 지정 된 드라이버 관련 정보는 손실 됩니다 및 **확인이 연결** 옵션 값은 캐시 되지 않습니다.)  
  
 경우 **파일 데이터 소스** 사용자 파일 이름을 입력 하 라는 메시지가 표시 드라이버를 선택한 후 키워드 값 고급 마법사 페이지에서 입력 한 다음 마법사의 첫 번째 페이지에서 선택 된입니다. 클릭 **찾아보기** 기본 디렉터리에 있는 경우 파일 이름에 대 한 검색 하는 **찾아보기** 상자 CommonFileDir HKEY_LOCAL_MACHINE\SOFTWARE\에 의해 지정 된 경로의 조합 하 여 지정 됩니다 Microsoft\Windows\CurrentVersion 및 "ODBC\DataSources"입니다. (CommonFileDir "C:\Program Files\Common Files" 되었으면 기본 디렉터리 것 "C:\Program Files\Common Files\ODBC\Data 원본"입니다.)  
  
 파일 이름이 입력 된 경우 및 **다음** 를 클릭 하면 파일 이름을 입력 한 운영 체제의 표준 파일 명명 규칙에 대해 유효한 지를 확인 합니다. 파일 이름이 유효 하지 않을 경우 오류 메시지 상자는 사용자에 게 알리는 잘못 된 파일 이름을 입력 했습니다. 사용자 승인 메시지 상자를 후 포커스 파일 이름이 입력 되어 마법사 페이지에 반환 됩니다. 파일 이름이 올바르면 다음 그림에 나와 있는 것 처럼 검토를 위해 선택한 키워드-값 쌍을 보여 주는 마법사 페이지가 표시 됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 검토](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 경우 **마침** 를 클릭 하 고 **파일 데이터 원본** 데이터 원본 유형으로 선택한 경우는 **이 연결을 확인** 옵션은 TRUE,  **SQLDriverConnect** 로 호출 되는 **SAVEFILE** 및 **드라이버** 키워드입니다. *DriverCompletion* 인수 SQL_DRIVER_COMPLETE로 설정 됩니다. 파일 이름에 대 한는 **SAVEFILE** 키워드는 입력 한 이름 또는 선택 함, 및에 대 한 드라이버 이름을 **드라이버** 키워드는 이름을 선택 합니다. 해당 문자열은 후 추가 고급 마법사 페이지로에 드라이버별 연결 문자열을 지정 하는 경우는 **드라이버** 키워드입니다.  
  
 경우 **SQLDriverConnect** 드라이버 관리자와 관계 없이 SQL_SUCCESS를 반환 파일 DSN을 만들었습니다. **SQLCreateDataSource** TRUE를 반환 합니다. 경우 **SQLDriverConnect** 경고 메시지와 관계 없이 SQL_SUCCESS를 반환 하지 않는 상자에 표시 된 연결을 데이터 원본에 설정할 수 없습니다. DSN이 지정 된 최소 연결 정보를 계속 만들 수 있습니다. 이 메시지 상자에는 취소 하거나 파일 DSN 만들기를 계속 사용자 수 있습니다.  
  
 이 프로세스를 계속 하는 경우에 사용자 DSN 만들기를 계속 하기로, 처럼는 **이 연결을 확인** 옵션이 FALSE로 설정 되었습니다. 에 대 한 FALSE가 반환 하는 경우 사용자가을 취소, **SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED의 오류 코드입니다.  
  
 경우 **파일 데이터 소스** 데이터 원본 유형으로 선택한 및 **이 연결을 확인** 옵션은 FALSE, 사용 하 여 파일 DSN 만들어집니다는 **드라이버** 키워드 및 사용자 지정 연결 문자열 (있는 경우)에서 고급 마법사 페이지로 합니다. 에 대 한 TRUE가 반환 되는 파일 만들기에 성공 하면 **SQLCreateDataSource**합니다. 파일 만들기 성공 하지 못한 경우 오류 메시지 상자 원인 오류는 운영 체제에서 반환 된 사용 하 여 사용자를 알립니다. 에 대 한 FALSE가 반환 **SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED의 오류 코드입니다. 파일 데이터 원본에 대 한 자세한 내용은 참조 [를 사용 하 여 파일 데이터 원본 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), 참조 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 경우 **사용자** 또는 **시스템 데이터 원본** 데이터 원본 유형으로 선택한 **ConfigDSN** 드라이버 설치 프로그램에서 라이브러리는 ODBC_ADD_DSN으로 호출  *문제점과*합니다. 자세한 내용은 참조 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터 소스 관리|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
