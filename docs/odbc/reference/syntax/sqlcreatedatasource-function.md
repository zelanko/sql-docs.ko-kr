---
title: SQLCreate데이터 소스 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94dc0d6d6f3b5bc96ae41aecda5b46f119cff85c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301203"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 함수
**규칙**  
 버전 출시: ODBC 2.0  
  
 **요약**  
 **SQLCreateDataSource는** 사용자가 데이터 원본을 추가할 수 있는 대화 상자를 표시합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>인수  
 *Hwnd*  
 [입력] 부모 창 핸들입니다.  
  
 *lpszDS*  
 [입력] 데이터 원본 이름입니다. *lpszDS는* null 포인터 또는 빈 문자열일 수 있습니다.  
  
## <a name="returns"></a>반환  
 **SQLCreateDataSource** 는 데이터 원본이 만들어지면 TRUE를 반환합니다. 그렇지 않으면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLCreateDataSource가** FALSE를 반환하는 경우 **SQLInstallerError**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못되었습니다.|*hwnd* 인수가 유효하지 않거나 NULL입니다.|  
|ODBC_ERROR_INVALID_DSN|잘못된 DSN|*lpszDS* 인수에는 DSN에 대해 유효하지 않은 문자열이 포함되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|ODBC_ADD_DSN 옵션을 사용하여 **ConfigDSN에** 대한 호출에 실패했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설정 라이브러리를 로드할 수 없습니다.|드라이버 설정 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_USER_CANCELED|사용자 취소 작업|새 데이터 원본 만들기를 취소했습니다.|  
|ODBC_ERROR_CREATE_DSN_FAILED|요청된 DSN을 만들 수 없습니다.|데이터베이스에 연결할 수 없습니다. 파일 DSN에 대한 **SQLDriverConnect** 호출이 성공적인 연결을 반환하지 않았습니다.<br /><br /> 파일에 쓸 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 *hwnd가* null이면 **SQLCreateDataSource는 FALSE를** 반환합니다. 그렇지 않으면 다음 그림과 같이 설정할 데이터 원본 유형을 선택하기 위한 마법사 페이지가 있는 **새 데이터 원본 만들기** 대화 상자가 표시됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 형식 선택](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 기본 옵션은 **파일 데이터 원본**입니다. 데이터 원본을 선택하고 **다음을** 클릭하면 설치된 드라이버 목록이 포함된 다음 마법사 페이지가 표시됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 드라이버 선택](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 **취소를** 클릭하면 대화 상자가 사라지고 **SQLCreateDataSource는** ODBC_ERROR_USER_CANCELED 오류 코드로 FALSE를 반환합니다. **사용자 데이터 원본** 또는 시스템 데이터 **원본** 옵션을 선택한 경우 **고급** 단추를 사용할 수 없습니다.  
  
 **다음** 단추를 클릭하면 선택한 데이터 원본 유형에 따라 다음 중 하나가 발생합니다.  
  
-   **파일 데이터 원본을** 선택한 경우 사용자가 파일 이름을 입력할 수 있는 마법사 페이지가 표시됩니다.  
  
-   사용자 **데이터 원본** 또는 **시스템 데이터 원본을** 선택한 경우 검토를 위해 데이터 원본 및 드라이버 의 형식을 표시하는 마법사 페이지가 표시되고 **완료를** 클릭하면 데이터 원본이 설정됩니다.  
  
 새 데이터 원본 만들기 마법사 페이지에서 **고급 을** 클릭하면 사용자가 드라이버 관련 정보를 입력할 수 있는 마법사 페이지가 표시됩니다. 이 대화 상자의 텍스트 상자에 다음 그림과 같이 반환으로 구분된 드라이버와 키워드를 입력합니다.  
  
 ![파일 DSN 만들기 고급 설정 대화 상자](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 추가 드라이버 관련 키워드는 **SQLDriverConnect**의 설명에서 찾을 수 있습니다. **DSN을** 제외한 모든 것이 허용됩니다.  
  
 이 연결 **확인** 옵션의 기본값은 TRUE입니다. 이 기본값은 이 마법사 페이지가 활성화되었는지 여부에 관계없이 적용됩니다. **확인을** 클릭하면 텍스트 상자에 지정된 문자열과 **이 연결 확인** 옵션 값이 캐시됩니다. 닫기 **Close** 단추 또는 **취소를** 클릭하면 텍스트 상자에 지정된 문자열과 **이 연결 확인** 옵션 값이 캐시되지 않으므로 새로 입력한 드라이버 관련 정보가 손실됩니다.  
  
 첫 번째 마법사 페이지에서 **파일 데이터 원본을** 선택한 다음 드라이버를 선택하고 고급 마법사 페이지에 키워드 값을 입력한 후 사용자에게 파일 이름을 입력하라는 메시지가 표시됩니다. **찾아보기를** 클릭하여 파일 이름을 검색하는 경우 **찾아보기** 상자의 기본 디렉토리가 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion 및 "ODBC\DataSource"에서 CommonFileDir에서 지정한 경로의 조합으로 지정됩니다. (CommonFileDir이 "C:\\프로그램 파일\일반 파일"인 경우 기본 디렉토리는 "C:\프로그램 파일\일반 파일\ODBC\데이터 원본"입니다.)  
  
 파일 이름을 입력하고 **다음을** 클릭하면 입력한 파일 이름이 운영 체제의 표준 파일 이름 지정 규칙에 대한 유효성을 검사합니다. 파일 이름이 잘못되면 오류 메시지 상자가 잘못된 파일 이름이 입력되었다는 것을 사용자에게 보신다. 사용자가 메시지 상자를 승인하면 포커스가 파일 이름이 입력된 마법사 페이지로 반환됩니다. 파일 이름이 유효한 경우 다음 그림과 같이 선택한 키워드 값 쌍을 표시하는 마법사 페이지가 검토를 위해 표시됩니다.  
  
 ![새 데이터 소스 만들기 대화 상자: 검토](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 **완료를** 클릭하고 **파일 데이터 원본을** 데이터 원본 유형으로 선택한 경우 **이 연결 확인** 옵션이 TRUE인 경우 **SQLDriverConnect는** **SAVEFILE** 및 **DRIVER** 키워드를 사용하여 호출됩니다. *드라이버완료* 인수가 SQL_DRIVER_COMPLETE 설정됩니다. **SAVEFILE** 키워드의 파일 이름은 입력하거나 선택한 이름이며 **DRIVER** 키워드의 드라이버 이름은 선택한 이름입니다. 고급 마법사 페이지에 드라이버 별 연결 문자열이 지정된 경우 해당 문자열은 **DRIVER** 키워드 다음쪽에 추가됩니다.  
  
 **SQLDriverConnect가** SQL_SUCCESS 반환하는 경우 드라이버 관리자가 파일 DSN을 만들었습니다. **SQLCreateDataSourceTRUE를** 반환합니다. **SQLDriverConnect가** SQL_SUCCESS 반환하지 않는 경우 경고 메시지 상자는 데이터 원본에 연결할 수 없다는 것을 나타냅니다. 연결 정보가 최소화된 DSN은 계속 만들 수 있습니다. 이 메시지 상자를 사용하면 파일 DSN 생성을 취소하거나 계속할 수 있습니다.  
  
 사용자가 DSN을 계속 만들도록 선택하면 **이 연결 확인** 옵션이 FALSE로 설정된 것처럼 이 프로세스가 계속됩니다. 사용자가 취소하도록 선택하면 오류 코드가 ODBC_ERROR_CREATE_DSN_FAILED **SQLCreateDataSource에** 대해 FALSE가 반환됩니다.  
  
 **파일 데이터 원본이** 데이터 원본 유형으로 선택되고 **이 연결 확인** 옵션이 FALSE인 경우 고급 마법사 페이지에서 **DRIVER** 키워드 및 사용자 지정 연결 문자열(있는 경우)으로 파일 DSN이 만들어집니다. 파일 생성에 성공하면 **TRUE가 SQLCreateDataSource**에 대해 반환됩니다. 파일 생성에 성공하지 못하면 오류 메시지 상자가 운영 체제에서 반환된 모든 오류를 사용자에게 보신다고 사용자에게 보신다. FALSE는 ODBC_ERROR_CREATE_DSN_FAILED 오류 코드와 **함께 SQLCreateDataSource에** 대해 반환됩니다. 파일 데이터 원본에 대한 자세한 내용은 [파일 데이터 원본 을 사용하여 연결을](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)참조하거나 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)를 참조하십시오.  
  
 **사용자** 또는 **시스템 데이터 원본이** 데이터 원본 유형으로 선택된 경우 드라이버 설정 라이브러리의 **ConfigDSN은** ODBC_ADD_DSN *fRequest를*사용하여 호출됩니다. 자세한 내용은 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)을 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본 관리|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
