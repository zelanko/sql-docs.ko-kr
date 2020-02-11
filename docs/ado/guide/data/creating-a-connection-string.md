---
title: 연결 문자열 만들기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c9d81ef7be98f3c65167de24b3ff59ac6f05df5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925762"
---
# <a name="creating-a-connection-string"></a>연결 문자열 만들기
연결 문자열은 세미콜론으로 구분 된 인수/값 쌍 (즉, 매개 변수)의 목록으로 구성 됩니다. 다음은 그 예입니다.  
  
```syntax
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 모든 매개 변수는 ADO 또는 지정 된 공급자에서 인식 되어야 합니다.  
  
 ADO는 연결 문자열에서 다음과 같은 5 개의 인수를 인식 합니다.  
  
|인수|Description|  
|--------------|-----------------|  
|*공급자*|연결에 사용할 공급자의 이름을 지정 합니다.|  
|*파일 이름*|미리 설정 된 연결 정보를 포함 하는 공급자별 파일 (예: 지속형 데이터 원본 개체)의 이름을 지정 합니다.|  
|*URL*|파일 또는 디렉터리와 같은 리소스를 식별 하는 절대 URL로 연결 문자열을 지정 합니다.|  
|*원격 공급자*|클라이언트 쪽 연결을 열 때 사용할 공급자의 이름을 지정 합니다. (원격 데이터 서비스에만 해당)|  
|*원격 서버*|클라이언트 쪽 연결을 열 때 사용할 서버의 경로 이름을 지정 합니다. (원격 데이터 서비스에만 해당)|  
  
 다른 인수는 ADO에서 처리 하지 않고 *공급자* 인수에서 라는 공급자에 전달 됩니다.  
  
 HelloData의 HelloData 응용 프로그램 [: 간단한 ADO 응용 프로그램](../../../ado/guide/data/hellodata-a-simple-ado-application.md) 은 다음 연결 문자열을 사용 했습니다.  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 이 연결 문자열에서 ADO는 SQL Server에 대 `"Provider=SQLOLEDB"` 한 Microsoft OLE DB 공급자를 ado 데이터 원본으로 지정 하는 매개 변수만 인식 합니다. 인수/값 쌍 `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`의 나머지가이 공급자에 게 전달 됩니다. 이러한 매개 변수의 유형 및 유효성 검사는 공급자별로 다릅니다. 연결 문자열에 전달 될 수 있는 유효한 매개 변수에 대 한 자세한 내용은 개별 공급자 설명서를 참조 하십시오.  
  
 SQL Server 설명서에 대 한 OLE DB 공급자에 따라 "Server"를 *데이터 원본* 매개 변수로 대체 하 고 "Database"를 *초기 카탈로그* 매개 변수에 사용할 수 있습니다. 따라서 다음 연결 문자열은 위의 결과와 동일한 결과를 생성 합니다.  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
