---
title: 데이터 소스 관리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6be8fba37a93e2fda66e96d1334ee4ddcb15d9e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32901718"
---
# <a name="managing-data-sources"></a>데이터 소스 관리
드라이버의 설치 프로그램에서 ODBC 드라이버를 설치한 후에 대 한 하나 이상의 데이터 원본을 정의할 수 있습니다. 데이터 원본 이름 (DSN)에서 데이터에 대 한 고유한 설명을 제공 해야 예를 들어 *급여* 또는 *Accounts Payable*합니다. 현재 설치 된 모든 드라이버에 대해 정의 된 사용자 및 시스템 데이터 원본은 나열 됩니다는 **사용자 DSN** 또는 **시스템 DSN** 의 탭에서 **ODBC 데이터 원본 관리자**대화 상자. 지정된 된 디렉터리의 파일 데이터 원본에 나열 됩니다는 **파일 DSN** ; 탭에 표시 되는 디렉터리를 입력의 **찾는 위치** 상자에 **파일 DSN** 탭 합니다.  
  
> [!NOTE]  
>  64 비트 플랫폼에서 32 비트 드라이버에 연결 하는 데이터 소스를 관리 하려면 c:\windows\sysWOW64\odbcad32.exe를 사용 합니다. 64 비트 드라이버에 연결 하는 데이터 소스를 관리 하려면 c:\windows\system32\odbcad32.exe를 사용 합니다. **관리 도구** 64 비트 Windows 8 운영 체제에는 32 비트 및 64 비트에 대 한 아이콘 **ODBC 데이터 원본 관리자** 대화 상자.  
  
 64 비트 odbcad32.exe를 사용 하 여 구성 하거나 예를 들어 32 비트 드라이버에 연결 하는 DSN을 제거할 경우 **드라이버 수행 됩니다 (\*.mdb)**, 다음과 같은 오류 메시지가 표시 됩니다.  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 이 오류를 해결 하려면 32 비트 odbcad32.exe를 사용 하 여 구성 하거나 DSN을 제거 합니다.  
  
 데이터 원본에 해당 드라이버를 통해 액세스 하려는 데이터와 특정 ODBC 드라이버를 연결 합니다. 예를 들어 하드 디스크 또는 네트워크 드라이브에서 특정 디렉터리에 있는 하나 이상의 dBASE 파일에 액세스 하려면 ODBC dBASE 드라이버를 사용 하도록 데이터 원본을 만들 수 있습니다. ODBC 데이터 원본 관리자를 사용 하 여 추가 수정 및 다음 표에 설명 된 대로 데이터 원본을 삭제 수 있습니다.  
  
|동작|Description|  
|------------|-----------------|  
|데이터 원본 추가|드라이버에 해당 드라이버를 사용 하 여 액세스 하려는 데이터 연결 하나씩 여러 데이터 소스를 추가할 수는 있습니다. 데이터 원본의 데이터 원본에 고유 하 게 식별 하는 이름을 제공 합니다. 예를 들어 고객 정보를 포함 하는 dBASE 파일 집합에 대 한 데이터 소스를 만드는 경우 데이터 원본 "Customers" 이름을 수 있습니다. 응용 프로그램에는 일반적으로 사용자가 선택할 수의 데이터 원본 이름을 표시 합니다.<br /><br /> 파일 데이터 원본을 추가 하는 것은 사용자 또는 시스템 데이터 원본 추가 약간 다릅니다. 자세한 내용은 ODBC 데이터 원본 관리자 도움말 파일을 참조 하십시오.|  
|데이터 원본 수정|요구 사항에 따라 필요할 수 있습니다이 데이터 원본을 다시 구성 해야 합니다. 옵션을 클릭 하 여 다시 설정할 수 있습니다 **구성** 모든 드라이버 설정 대화 상자에서 합니다.|  
|데이터 원본 삭제|클릭 **제거** 데이터 원본을 선택한 후 합니다.|  
  
 파일 데이터 원본에 대 한 자세한 내용은 참조 [를 사용 하 여 파일 데이터 원본 연결](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) 또는 [SQLDriverConnect 함수](../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md)
