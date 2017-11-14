---
title: "연결 문자열 만들기 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 90105b448604f3b99fefc2598fa375677f0bbdb4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="creating-a-connection-string"></a>연결 문자열 만들기
연결 문자열을 세미콜론으로 구분 된 인수/값 쌍 (즉, 매개 변수)의 목록으로 구성 합니다. 예를 들어  
  
```  
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 모든 매개 변수는 ADO 또는 지정된 된 공급자에서 인식 되어야 합니다.  
  
 ADO 연결 문자열에는 다음 5 개 인수를 인식합니다.  
  
|인수|Description|  
|--------------|-----------------|  
|*공급자*|연결에 사용할 공급자의 이름을 지정 합니다.|  
|*파일 이름*|미리 설정 된 연결 정보를 포함 하는 공급자별 파일 (예를 들어 지속형된 데이터 원본 개체)의 이름을 지정 합니다.|  
|*URL*|파일 또는 디렉터리와 같은 리소스를 식별 하는 절대 URL로 연결 문자열을 지정 합니다.|  
|*원격 공급자*|클라이언트 연결을 열 때 사용할 공급자의 이름을 지정 합니다. (원격 데이터 서비스만 합니다.)|  
|*원격 서버*|클라이언트 연결을 열 때 사용할 서버 경로 이름을 지정 합니다. (원격 데이터 서비스만 합니다.)|  
  
 다른 인수에 지정 된 공급자에 전달 되는 *공급자* ADO에서 처리 없이 인수입니다.  
  
 HelloData 응용 프로그램에 [HelloData: 간단한 ADO 응용 프로그램](../../../ado/guide/data/hellodata-a-simple-ado-application.md) 다음 연결 문자열을 사용 합니다.  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 이 연결 문자열에 ADO만 인식는 `"Provider=SQLOLEDB"` ADO 데이터 원본으로 SQL Server 용 Microsoft OLE DB Provider를 지정 하는 매개 변수입니다. 인수/값 쌍의 나머지 부분 `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`,이 공급자에 정확 하 게 전달 됩니다. 형식 및 이러한 매개 변수가의 유효성은 공급자 마다 다릅니다. 연결 문자열에 전달 될 수 있는 유효한 매개 변수에 대 한 정보, 개별 공급 업체의 설명서를 참조 하십시오.  
  
 OLE DB Provider for SQL Server 설명서에 따라 대신 사용할 수 있습니다 "Server"는 *데이터 소스* 매개 변수 및 "데이터베이스"에 대 한는 *초기 카탈로그* 매개 변수입니다. 따라서 다음 연결 문자열은 위와 동일한 결과가 발생 합니다.  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```

