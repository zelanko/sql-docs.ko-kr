---
title: 드라이버 관련 연결 정보 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3852e713e517828e83e74bf7fb291ef20865532
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238709"
---
# <a name="driver-specific-connection-information"></a>드라이버별 연결 정보
**SQLConnect** 가정 하는 데이터 원본 이름, 사용자 ID 및 암호는 데이터 원본에 연결 하기에 충분 하 고 시스템에 다른 모든 연결 정보를 저장할 수 있습니다. 이 경우가 자주 있습니다. 예를 들어, DBMS에 로그온 할 때 서버 및 다른 사용자 ID 및 암호에 로그온 한 사용자 ID와 암호는 드라이버가 필요할 수 있습니다. 때문에 **SQLConnect** 단일 사용자 ID와 암호를 허용 합니다. 즉,는 다른 사용자 ID 및 암호를 저장 해야 시스템에서 데이터 원본 정보를 사용 하 여 **SQLConnect** 사용할 합니다. 잠재적인 보안 위반 하는 암호를 암호화 하지 않는 한 피해 야 합니다.  
  
 **SQLDriverConnect** 드라이버에서 연결 문자열 키워드-값 쌍의 임의 크기의 연결 정보를 정의할 수 있습니다. 예를 들어, 드라이버 경우 dbms 서버 및 사용자 ID 및 암호에 대 한 데이터 원본 이름, 사용자 ID 및 암호 필요 합니다. 항상 XYZ Corp 데이터 소스를 사용 하는 사용자 지정 프로그램 Id 및 암호를 묻는 메시지를 수 있습니다 및 키워드-값 쌍의 다음 집합을 작성 하거나 *연결 문자열* 에 전달할 **SQLDriverConnect**:  
  
> [!NOTE]  
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, `Trusted_Connection=yes` 연결 문자열에 사용자 ID와 암호 정보 대신 합니다.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** (데이터 원본 이름) 키워드 이름을 데이터 원본에는 **UID** 하 고 **PWD** 키워드는 사용자 ID 및 서버에 대 한 암호를 지정 및 **UIDDBMS**  하 고 **PWDDBMS** DBMS에 대 한 사용자 ID 및 암호를 지정 하는 키워드입니다. 최종 세미콜론 선택 사항 인지 확인 합니다. **SQLDriverConnect** ;이 문자열을 구문 분석 하 고, 서버 주소; 같은 시스템에서 추가 연결 정보를 검색할 XYZ Corp 데이터 원본 이름을 사용 하 고, DBMS 지정 된 사용자 Id 및 암호를 사용 하 고 서버에 로그온 합니다.  
  
 키워드-값 쌍 **SQLDriverConnect** 특정 구문 규칙을 따라야 합니다. 키워드 및 해당 값 포함 하지 않아야 합니다 **{}(),? \*=! @** 문자입니다. 값을 **DSN** 키워드를 공백으로 구성할 수 없습니다 및 선행 공백을 포함 하지 않아야 합니다. 레지스트리 문법으로 인해 키워드 및 데이터 원본 이름은 백슬래시를 포함할 수 없습니다 (\\) 문자입니다. 키워드-값 쌍에서 등호 앞뒤 공백은 허용 되지 않습니다.  
  
 합니다 **FILEDSN** 호출에서 키워드를 사용할 수 있습니다 **SQLDriverConnect** 데이터 원본 정보를 포함 하는 파일의 이름을 지정 하려면 (참조 [연결 파일을 데이터 원본 사용](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)이 섹션의 뒷부분에 나오는). 합니다 **SAVEFILE** 호출에 의해 성공적으로 연결의 키워드-값 쌍을 수행 하는.dsn 파일의 이름을 지정 하려면 키워드를 사용할 수 있습니다 **SQLDriverConnect** 저장 됩니다. 파일 데이터 원본에 대 한 자세한 내용은 참조는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.
