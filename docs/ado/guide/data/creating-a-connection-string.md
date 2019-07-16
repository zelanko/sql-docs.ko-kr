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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925762"
---
# <a name="creating-a-connection-string"></a>연결 문자열 만들기
연결 문자열 (즉, 매개 변수) 인수/값 쌍의 세미콜론으로 구분 된 목록으로 구성 됩니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```syntax
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 모든 매개 변수는 ADO 또는 지정된 된 공급자 중 하나에서 인식 되어야 합니다.  
  
 ADO 연결 문자열에는 다음 5 개 인수를 인식합니다.  
  
|인수|설명|  
|--------------|-----------------|  
|*공급자*|연결에 사용할 공급자의 이름을 지정 합니다.|  
|*파일 이름*|미리 설정 된 연결 정보를 포함 하는 공급자별 파일 (예를 들어 지속형된 데이터 원본 개체)의 이름을 지정 합니다.|  
|*URL*|파일 또는 디렉터리와 같은 리소스를 식별 하는 절대 URL로 연결 문자열을 지정 합니다.|  
|*원격 공급자*|클라이언트 쪽 연결을 열 때 사용할 공급자의 이름을 지정 합니다. (원격 데이터 서비스만 해당입니다.)|  
|*원격 서버*|클라이언트 쪽 연결을 열 때 사용할 서버를의 경로 이름을 지정 합니다. (원격 데이터 서비스만 해당입니다.)|  
  
 다른 인수에서 명명 된 공급자에 전달 되는 *공급자* ADO에서 처리 하지 않고 인수입니다.  
  
 HelloData 응용 프로그램 [HelloData: 간단한 ADO 응용 프로그램을](../../../ado/guide/data/hellodata-a-simple-ado-application.md) 다음 연결 문자열을 사용 합니다.  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 이 연결 문자열에 ADO만 인식 합니다 `"Provider=SQLOLEDB"` ADO 데이터 원본으로 SQL Server 용 Microsoft OLE DB Provider를 지정 하는 매개 변수입니다. 인수/값 쌍을 나머지 `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`,이 공급자를 정확 하 게 전달 됩니다. 형식 및 이러한 매개 변수의 유효성은 공급자 마다 다릅니다. 연결 문자열에 전달 될 수 있는 유효한 매개 변수에 대 한 자세한 내용은 개별 공급자의 설명서를 참조 하세요.  
  
 OLE DB Provider for SQL Server 설명서를 따라 대체할 수 "Server"를 *데이터 원본* 매개 변수 및 "데이터베이스"에 대 한 합니다 *Initial Catalog* 매개 변수입니다. 따라서 다음 연결 문자열은 위와 동일한 결과가 발생 합니다.  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
