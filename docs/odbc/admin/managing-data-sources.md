---
description: 데이터 원본 관리
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 506a7b6fbbf93b8fb4b28f66824778b2266f6cbc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412866"
---
# <a name="managing-data-sources"></a>데이터 원본 관리
드라이버의 설치 프로그램에서 ODBC 드라이버를 설치한 후에는 하나 이상의 데이터 원본을 정의할 수 있습니다. 데이터 원본 이름 (DSN)은 데이터에 대 한 고유한 설명을 제공 해야 합니다. 예: *급여* 또는 *외상 매입금*. 현재 설치 된 모든 드라이버에 대해 정의 된 사용자 및 시스템 데이터 원본은 **ODBC 데이터 원본 관리자** 대화 상자의 **사용자 DSN** 또는 **시스템 dsn** 탭에 나열 됩니다. 지정 된 디렉터리의 파일 데이터 원본이 **파일 DSN** 탭에 나열 됩니다. 표시 되는 디렉터리는 **파일 DSN** 탭의 **찾는 위치** 상자에 입력 됩니다.  
  
> [!NOTE]  
>  64 비트 플랫폼에서 32 비트 드라이버에 연결 하는 데이터 원본을 관리 하려면 c:\windows\sysWOW64\odbcad32.exe을 사용 합니다. 64 비트 드라이버에 연결 하는 데이터 원본을 관리 하려면 c:\windows\system32\odbcad32.exe을 사용 합니다. 64 비트 Windows 8 운영 체제의 **관리 도구** 에는 32 비트 및 64 비트 **ODBC 데이터 원본 관리자** 대화 상자 둘 다에 대 한 아이콘이 있습니다.  
  
 64 비트 odbcad32.exe를 사용 하 여 32 비트 드라이버에 연결 하는 DSN을 구성 하거나 제거 하는 경우, 예를 들어 **Driver Microsoft Access ( \* .mdb)** 를 사용 하는 경우 다음 오류 메시지가 표시 됩니다.  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 이 오류를 해결 하려면 32 비트 odbcad32.exe를 사용 하 여 DSN을 구성 하거나 제거 합니다.  
  
 데이터 원본은 특정 ODBC 드라이버를 해당 드라이버를 통해 액세스 하려는 데이터와 연결 합니다. 예를 들어 ODBC dBASE 드라이버를 사용 하 여 하드 디스크 또는 네트워크 드라이브의 특정 디렉터리에 있는 하나 이상의 dBASE 파일에 액세스 하는 데이터 원본을 만들 수 있습니다. ODBC 데이터 원본 관리자를 사용 하 여 다음 표에 설명 된 대로 데이터 원본을 추가, 수정 및 삭제할 수 있습니다.  
  
|작업|설명|  
|------------|-----------------|  
|데이터 원본 추가|여러 데이터 원본을 추가할 수 있습니다. 각각은 드라이버를 해당 드라이버를 사용 하 여 액세스 하려는 일부 데이터와 연결 합니다. 각 데이터 원본에 해당 데이터 원본을 고유 하 게 식별 하는 이름을 지정 합니다. 예를 들어 고객 정보를 포함 하는 dBASE 파일 집합에 대 한 데이터 원본을 만드는 경우 데이터 원본의 이름을 "Customers"로 설정할 수 있습니다. 응용 프로그램은 일반적으로 사용자가 선택할 수 있는 데이터 원본 이름을 표시 합니다.<br /><br /> 파일 데이터 원본을 추가 하는 것은 사용자 또는 시스템 데이터 원본을 추가 하는 것과 약간 다릅니다. 자세한 내용은 ODBC 데이터 원본 관리자 도움말 파일을 참조 하십시오.|  
|데이터 원본 수정|요구 사항에 따라 데이터 원본을 다시 구성 해야 할 수도 있습니다. 모든 드라이버 설치 대화 상자에서 **구성** 을 클릭 하 여 옵션을 다시 설정할 수 있습니다.|  
|데이터 원본 삭제|데이터 원본을 선택한 후 **제거** 를 클릭 합니다.|  
  
 파일 데이터 원본에 대 한 자세한 내용은 파일 데이터 원본 또는 [SQLDriverConnect 함수](../../odbc/reference/syntax/sqldriverconnect-function.md)를 [사용 하 여 연결](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) 을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md)
