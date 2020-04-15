---
title: 드라이버 별 연결 정보 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16c8c5fc4fd3ac63aa3613b41e530446dffec118
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305794"
---
# <a name="driver-specific-connection-information"></a>드라이버별 연결 정보
**SQLConnect는** 데이터 원본 이름, 사용자 ID 및 암호가 데이터 원본에 연결하기에 충분하고 다른 모든 연결 정보가 시스템에 저장될 수 있다고 가정합니다. 이 경우는 그렇지 않은 경우가 자주 있습니다. 예를 들어 드라이버가 서버에 로그온하려면 하나의 사용자 ID와 암호가 필요하고 DBMS에 로그온하려면 다른 사용자 ID와 암호가 필요할 수 있습니다. **SQLConnect는** 단일 사용자 ID와 암호를 허용하므로 **SQLConnect를** 사용하려면 다른 사용자 ID와 암호를 시스템의 데이터 원본 정보와 함께 저장해야 합니다. 이는 보안 위반일 수 있으며 암호가 암호화되지 않는 한 피해야 합니다.  
  
 **SQLDriverConnect를** 사용하면 드라이버가 연결 문자열의 키워드 값 쌍에서 임의의 양의 연결 정보를 정의할 수 있습니다. 예를 들어 드라이버에 데이터 원본 이름, 서버의 사용자 ID 및 암호, DBMS의 사용자 ID 및 암호가 필요하다고 가정합니다. 항상 XYZ Corp 데이터 원본을 사용하는 사용자 지정 프로그램은 사용자에게 ID와 암호를 묻고 다음 키워드 값 쌍 또는 *연결 문자열* 집합을 빌드하여 **SQLDriverConnect에**전달할 수 있습니다.  
  
> [!NOTE]  
>  Windows 인증을 지원하는 데이터 원본 공급자에 연결하는 경우 `Trusted_Connection=yes` 연결 문자열에서 사용자 ID 및 암호 정보 대신 지정해야 합니다.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN(데이터** 원본 이름) 키워드는 데이터 원본의 이름을 지정하고 **UID** 및 **PWD** 키워드는 서버의 사용자 ID와 암호를 지정하고 **UIDDBMS** 및 **PWDDBMS** 키워드는 DBMS의 사용자 ID와 암호를 지정합니다. 최종 세미콜론은 선택 사항입니다. **SQLDriverConnect는** 이 문자열을 구문 분석합니다. XYZ Corp 데이터 원본 이름을 사용하여 서버 주소와 같은 시스템에서 추가 연결 정보를 검색합니다. 지정된 사용자 ID와 암호를 사용하여 서버 및 DBMS에 로그온합니다.  
  
 **SQLDriverConnect의** 키워드 값 쌍은 특정 구문 규칙을 따라야 합니다. 키워드와 해당 값은 **[]{}(;;)를 포함해서는 안 됩니다. \*=!@** 문자. **DSN** 키워드의 값은 공백으로만 구성될 수 없으며 선행 공백을 포함해서는 안 됩니다. 레지스트리 문법으로 인해 키워드 및 데이터 원본 이름은 백슬래시()\\문자를 포함할 수 없습니다. 키워드 값 쌍의 등호 주위에 공백은 허용되지 않습니다.  
  
 **FILEDSN** 키워드는 **SQLDriverConnect** 를 호출하여 데이터 원본 정보가 포함된 파일의 이름을 지정하는 데 사용할 수 있습니다(이 섹션의 다음 부분의 파일 [데이터 원본 사용 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)참조). **SAVEFILE** 키워드를 사용하여 **SQLDriverConnect** 호출에 의해 성공적으로 연결한 키워드 값 쌍이 저장되는 .dsn 파일의 이름을 지정할 수 있습니다. 파일 데이터 원본에 대한 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조하십시오.
