---
title: 데이터 원본 관리 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9dc741321894ae69a9ffb59738576a01d47628f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901665"
---
# <a name="managing-data-sources"></a>데이터 원본 관리
드라이버의 설치 프로그램에서 ODBC 드라이버를 설치한 후에 대 한 하나 이상의 데이터 원본을 정의할 수 있습니다. 데이터 원본 이름 (DSN)에 데이터의 고유한 설명을 제공 해야 예를 들어 *급여* 하거나 *Accounts Payable*합니다. 현재 설치 된 모든 드라이버에 대해 정의 된 사용자 및 시스템 데이터 원본에 나열 됩니다는 **사용자 DSN** 또는 **시스템 DSN** 탭을 **ODBC 데이터 원본 관리자**대화 상자. 지정된 된 디렉터리의 파일 데이터 원본에 나열 됩니다는 **파일 DSN** 탭을 표시할 디렉터리에 입력를 **찾는 위치** 상자에 **파일 DSN** 탭 합니다.  
  
> [!NOTE]  
>  64 비트 플랫폼에서 32 비트 드라이버에 연결 하는 데이터 소스를 관리 하려면 c:\windows\sysWOW64\odbcad32.exe를 사용 합니다. 64 비트 드라이버에 연결 하는 데이터 소스를 관리 하려면 c:\windows\system32\odbcad32.exe를 사용 합니다. **관리 도구** 64 비트 Windows 8 운영 체제는 32 비트 및 64 비트에 대 한 아이콘 **ODBC 데이터 원본 관리자** 대화 상자.  
  
 구성 하거나 예를 들어 32 비트 드라이버를 연결 하는 DSN을 제거 하려면 64 비트 odbcad32.exe를 사용 하는 경우 **드라이버 수행 됩니다 (\*.mdb)** , 다음 오류 메시지가 나타납니다.  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 이 오류를 해결 하려면 구성 하거나 DSN을 제거 하려면 32 비트 odbcad32.exe를 사용 합니다.  
  
 데이터 원본에 해당 드라이버를 통해 액세스 하려는 데이터를 사용 하 여 특정 ODBC 드라이버를 연결 합니다. 예를 들어 ODBC dBASE 드라이버 특정 디렉터리 하드 디스크 또는 네트워크 드라이브에 있는 하나 이상의 dBASE 파일 액세스를 사용 하는 데이터 소스를 만들 수 있습니다. ODBC 데이터 원본 관리자를 사용 하 여, 있습니다 수 추가, 수정 및 삭제 데이터 원본에 다음 표에 설명 된 대로 합니다.  
  
|Action|설명|  
|------------|-----------------|  
|데이터 원본 추가|드라이버는 드라이버를 사용 하 여 액세스 하려는 일부 데이터를 사용 하 여 연결 각각 여러 데이터 소스를 추가 하는 것이 가능 합니다. 각 데이터 원본의 해당 데이터 소스를 고유 하 게 식별 하는 이름을 지정 합니다. 예를 들어 고객 정보를 포함 하는 dBASE 파일 집합에 대 한 데이터 소스를 만드는 경우 이름을 지정할 수 있습니다 데이터 원본 "고객"을 선택 합니다. 응용 프로그램에는 일반적으로 사용자가 선택할 수에 대 한 데이터 원본 이름이 표시 됩니다.<br /><br /> 파일 데이터 원본을 추가 하는 것은 사용자 또는 시스템 데이터 원본 추가에서 약간 다릅니다. 자세한 내용은 ODBC 데이터 원본 관리자 도움말 파일을 참조 하세요.|  
|데이터 원본 수정|요구 사항에 따라 필요할 수 있습니다이 데이터 원본을 다시 구성 합니다. 클릭 하 여 옵션을 다시 설정할 수 있습니다 **구성** 모든 드라이버 설치 대화 상자에서.|  
|데이터 원본 삭제|클릭 **제거** 후 데이터 원본을 선택 합니다.|  
  
 파일 데이터 원본에 대 한 자세한 내용은 참조 하세요. [를 사용 하 여 파일 데이터 원본에 연결](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) 또는 [SQLDriverConnect 함수](../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md)
