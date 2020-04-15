---
title: 데이터 소스 관리 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5069ac9a5babc3071c52d73d5b56b21729a5d8a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307214"
---
# <a name="managing-data-sources"></a>데이터 원본 관리
드라이버의 설치 프로그램에서 ODBC 드라이버를 설치한 후 하나 이상의 데이터 원본을 정의할 수 있습니다. 데이터 원본 이름(DSN)은 데이터에 대한 고유한 설명을 제공해야 합니다. 예를 들어, *급여* 또는 *미지급금.* 현재 설치된 모든 드라이버에 대해 정의된 사용자 및 시스템 데이터 원본은 **ODBC 데이터 원본 관리자** 대화 상자의 사용자 **DSN** 또는 **시스템 DSN** 탭에 나열됩니다. 지정된 디렉터리에서 파일 데이터 원본이 **파일 DSN** 탭에 나열됩니다. 표시할 디렉토리가 **파일 DSN** 탭의 **보기 상자에** 입력됩니다.  
  
> [!NOTE]  
>  64비트 플랫폼에서 32비트 드라이버에 연결하는 데이터 원본을 관리하려면 c:\windows\sysWOW64\odbcad32.exe를 사용합니다. 64비트 드라이버에 연결하는 데이터 원본을 관리하려면 c:\windows\system32\odbcad32.exe를 사용합니다. 64비트 Windows 8 운영 체제의 **관리 도구에는** 32비트 및 64비트 **ODBC 데이터 원본 관리자** 대화 상자에 대한 아이콘이 있습니다.  
  
 64비트 odbcad32.exe를 사용하여 32비트 드라이버에 연결되는 DSN을 구성하거나 제거하는 경우(예: **드라이버는 Microsoft\*Access(.mdb)를**수행하므로 다음과 같은 오류 메시지가 나타납니다.  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 이 오류를 해결하려면 32비트 odbcad32.exe를 사용하여 DSN을 구성하거나 제거합니다.  
  
 데이터 원본은 특정 ODBC 드라이버를 해당 드라이버를 통해 액세스하려는 데이터와 연결합니다. 예를 들어 ODBC dBASE 드라이버를 사용하여 하드 디스크 또는 네트워크 드라이브의 특정 디렉터리에 있는 하나 이상의 dBASE 파일에 액세스하기 위해 데이터 원본을 만들 수 있습니다. ODBC 데이터 원본 관리자를 사용하여 다음 표에 설명된 대로 데이터 원본을 추가, 수정 및 삭제할 수 있습니다.  
  
|작업|설명|  
|------------|-----------------|  
|데이터 원본 추가|여러 데이터 원본을 추가할 수 있으며, 각 데이터 원본은 해당 드라이버를 사용하여 액세스하려는 일부 데이터와 드라이버를 연결합니다. 각 데이터 원본에 해당 데이터 원본을 고유하게 식별하는 이름을 지정합니다. 예를 들어 고객 정보가 포함된 dBASE 파일 집합에 대한 데이터 원본을 만드는 경우 데이터 원본의 이름을 "고객"으로 지정할 수 있습니다. 응용 프로그램은 일반적으로 사용자가 선택할 수 있는 데이터 원본 이름을 표시합니다.<br /><br /> 파일 데이터 원본을 추가하는 것은 사용자 또는 시스템 데이터 원본을 추가하는 경우와 약간 다릅니다. 자세한 내용은 ODBC 데이터 원본 관리자 도움말 파일을 참조하세요.|  
|데이터 원본 수정|요구 사항에 따라 데이터 원본을 다시 구성하는 것이 필요할 수 있습니다. 드라이버 설정 대화 상자에서 **구성을** 클릭하여 옵션을 재설정할 수 있습니다.|  
|데이터 원본 삭제|데이터 원본을 선택한 후 **제거를** 클릭합니다.|  
  
 파일 데이터 원본에 대한 자세한 내용은 파일 데이터 원본 또는 [SQLDriverConnect 함수를](../../odbc/reference/syntax/sqldriverconnect-function.md) [사용하여 연결을](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md)
