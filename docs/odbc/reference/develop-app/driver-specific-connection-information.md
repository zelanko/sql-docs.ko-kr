---
description: 드라이버별 연결 정보
title: 드라이버별 연결 정보 | Microsoft Docs
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
ms.openlocfilehash: f026349b4146a37c680185cdeb1d6e2066665222
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483036"
---
# <a name="driver-specific-connection-information"></a>드라이버별 연결 정보
**SQLConnect** 는 데이터 원본 이름, 사용자 ID 및 암호가 데이터 원본에 연결 하기에 충분 하 고 다른 모든 연결 정보가 시스템에 저장 될 수 있다고 가정 합니다. 이는 대부분의 경우는 아닙니다. 예를 들어, 서버에 로그온 하려면 한 사용자 ID와 암호를 사용 하 고 DBMS에 로그온 하려면 다른 사용자 id와 암호를 사용 해야 할 수 있습니다. **SQLConnect** 는 단일 사용자 id와 암호를 허용 하므로 **SQLConnect** 를 사용할 경우 다른 사용자 id와 암호를 시스템의 데이터 원본 정보와 함께 저장 해야 함을 의미 합니다. 이는 보안의 잠재적 위반 이며 암호를 암호화 하지 않는 한 피해 야 합니다.  
  
 **SQLDriverConnect** 를 사용 하면 드라이버에서 연결 문자열의 키워드-값 쌍에 임의의 연결 정보를 정의할 수 있습니다. 예를 들어 데이터 원본 이름, 서버의 사용자 ID 및 암호, DBMS의 사용자 ID 및 암호를 요구 하는 드라이버가 있다고 가정 합니다. 항상 XYZ Corp 데이터 원본을 사용 하는 사용자 지정 프로그램은 사용자에 게 Id 및 암호를 묻는 메시지를 표시 하 고 다음과 같은 키워드-값 쌍 또는 *연결 문자열* 집합을 작성 하 여 **SQLDriverConnect**에 전달할 수 있습니다.  
  
> [!NOTE]  
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 `Trusted_Connection=yes` 연결 문자열에 사용자 ID 및 암호 정보를 지정 하는 대신를 지정 해야 합니다.  
  
```  
DSN={MyDataSourceName};UID={MyUserID};PWD={MyServerPassword};UIDDBMS={MyDBMSUserID};PWDDBMS={MyDBMSUserPassword};  
```  
  
 **DSN** (데이터 원본 이름) 키워드는 데이터 원본의 이름을 지정 하 고 **UID** 및 **PWD** 키워드는 서버에 대 한 사용자 Id와 암호를 지정 하며 **UIDDBMS** 및 **pwddbms** 키워드는 DBMS에 대 한 사용자 id와 암호를 지정 합니다. 마지막 세미콜론은 선택 사항입니다. **SQLDriverConnect** 는이 문자열을 구문 분석 합니다. 는 XYZ Corp 데이터 원본 이름을 사용 하 여 서버 주소와 같은 시스템에서 추가 연결 정보를 검색 합니다. 및는 지정 된 사용자 Id와 암호를 사용 하 여 서버 및 DBMS에 로그온 합니다.  
  
 **SQLDriverConnect** 의 키워드-값 쌍은 특정 구문 규칙을 따라야 합니다. 키워드와 해당 값은 **[] {} (),;? \* 를 포함할 수 없습니다. =! @** 문자. **DSN** 키워드의 값은 공백으로만 구성 될 수 없으며 선행 공백을 포함할 수 없습니다. 레지스트리 문법 때문에 키워드와 데이터 원본 이름에는 백슬래시 () 문자를 사용할 수 없습니다 \\ . 키워드-값 쌍의 등호 앞뒤에는 공백을 사용할 수 없습니다.  
  
 **Filedsn** 키워드는 **SQLDriverConnect** 에 대 한 호출에서 사용 하 여 데이터 소스 정보를 포함 하는 파일의 이름을 지정할 수 있습니다 (이 섹션의 뒷부분에 나오는 [파일 데이터 원본을 사용 하 여 연결](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)참조). **SAVEFILE** 키워드를 사용 하 여 **SQLDriverConnect** 에 대 한 호출로 성공한 연결의 키워드-값 쌍을 저장 하는 dsn 파일의 이름을 지정할 수 있습니다. 파일 데이터 원본에 대 한 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조 하세요.
