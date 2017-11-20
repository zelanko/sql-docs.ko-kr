---
title: "드라이버 관련 연결 정보 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConnect function [ODBC], driver-specific connection information
- connecting to driver [ODBC], SQLConnect
- SQLDriverConnect function [ODBC], driver specific connection information
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SQLConnect
- connecting to driver [ODBC], driver-specific information
ms.assetid: 3748758a-f16a-4f3b-9c40-06f2e300704e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9e1624febc9b53c654c1b01f5aafb601b97b3cbf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="driver-specific-connection-information"></a>드라이버 관련 연결 정보
**SQLConnect** 가정 하는 데이터 원본 이름, 사용자 ID 및 암호는 데이터 원본에 연결 하기에 충분 하 고 다른 모든 연결 정보는 시스템에 저장할 수 있습니다. 이 경우가 자주 있습니다. 예를 들어 한 사용자 ID와 암호 DBMS에 로그온 하는 서버 및 다른 사용자 ID 및 암호에 로그온 할 수는 드라이버 해야 합니다. 때문에 **SQLConnect** 단일 사용자 ID와 암호를 허용 합니다. 즉,는 다른 사용자 ID와 암호를 저장 해야 시스템에 데이터 소스 정보로 **SQLConnect** 사용할 합니다. 잠재적인 보안 위반 이며 암호를 암호화 하지 않는 한 피해 야 합니다.  
  
 **SQLDriverConnect** 드라이버에서 연결 문자열 키워드-값 쌍에서 임의 크기의 연결 정보를 정의할 수 있습니다. 예를 들어, 드라이버 경우 DBMS에 대 한 서버 및 사용자 ID와 암호에 대 한 데이터 원본 이름, 사용자 ID 및 암호가 필요 합니다. 항상 XYZ Corp 데이터 원본을 사용 하는 사용자 지정 프로그램 수 사용자 Id 및 암호를 묻는 메시지를 한 키워드-값 쌍의 다음 집합을 작성 또는 *연결 문자열* 에 전달할 **SQLDriverConnect**:  
  
> [!NOTE]  
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, `Trusted_Connection=yes` 연결 문자열에 사용자 ID와 암호 정보 대신 합니다.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** 데이터 원본 이름을 지정 (데이터 원본 이름) 키워드는 **UID** 및 **PWD** 사용자 ID와 서버에 대 한 암호를 지정 하는 키워드와 **UIDDBMS**  및 **PWDDBMS** 키워드는 DBMS에 대 한 사용자 ID와 암호를 지정 합니다. 최종 세미콜론은 선택 사항 확인 합니다. **SQLDriverConnect** 이 문자열을 구문 분석; XYZ Corp 데이터 원본 이름을 사용 하 여 서버 주소; 같은 시스템에서 추가 연결 정보를 검색 하 고, 서버 및 지정 된 사용자 Id와 암호를 사용 하 여 DBMS에 로그온 합니다.  
  
 키워드-값 쌍 **SQLDriverConnect** 특정 구문 규칙을 따라야 합니다. 키워드와 값 포함 되 면 안는 **{} (),? \*=! @** 문자입니다. 값은 **DSN** 키워드는 공백으로 구성할 수 없습니다 및 선행 공백을 포함할 수 없습니다. 키워드 및 데이터 원본 이름 레지스트리 문법 때문에 백슬래시를 포함할 수 없습니다 (\\) 문자. 키워드 / 값 쌍의 등호 엔 공백이 허용 되지 않습니다.  
  
 **FILEDSN** 키워드에 대 한 호출에서 사용할 수 있습니다 **SQLDriverConnect** 데이터 원본 정보를 포함 하는 파일의 이름을 지정 하려면 (참조 [연결 파일을 데이터 원본 사용](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)이 섹션의 뒷부분에 나오는). **SAVEFILE** 에 대 한 호출에서 성공적인 연결 키워드-값 쌍 구성.dsn 파일의 이름을 지정 하려면 키워드를 사용할 수 있습니다 **SQLDriverConnect** 저장 됩니다. 파일 데이터 원본에 대 한 자세한 내용은 참조는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.

