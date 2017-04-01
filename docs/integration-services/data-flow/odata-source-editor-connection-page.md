---
title: "OData 원본 편집기(연결 페이지) | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.odatasource.connection.f1"
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# OData 원본 편집기(연결 페이지)
  **OData 원본 편집기** 대화 상자의 **연결** 페이지를 사용하여 OData 원본의 OData 연결 관리자를 선택할 수 있습니다. 또한 이 페이지에서 컬렉션 또는 리소스 경로와 쿼리 옵션을 지정하여 OData 원본에서 검색해야 하는 데이터를 나타낼 수 있습니다. OData 원본에 대한 자세한 내용은 [OData Source](../../integration-services/data-flow/odata-source.md)을 참조하십시오.  
  
## 정적 옵션  
 **OData 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 연결 관리자를 선택하거나 만든 후 대화 상자는 연결 관리자가 사용하는 OData 프로토콜 버전을 표시합니다.  
  
 **새로 만들기**  
 **OData 연결 관리자 편집기** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **컬렉션 또는 리소스 경로 사용**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|컬렉션|컬렉션 이름을 사용하여 OData 원본에서 데이터를 검색합니다.|  
|리소스 경로|리소스 경로를 사용하여 OData 원본에서 데이터를 검색합니다.|  
  
 **쿼리 옵션**  
 쿼리에 대한 옵션을 지정합니다.  예: $top=5  
  
 **피드 URL**  
 이 대화 상자에서 선택한 옵션에 따라 읽기 전용 피드 URL을 표시합니다.  
  
 **미리 보기**  
 **미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. **미리 보기** 에는 최대 20개의 행이 표시될 수 있습니다.  
  
## 동적 옵션  
  
### 컬렉션 또는 리소스 경로 사용 = 컬렉션  
 **컬렉션**  
 드롭다운 목록에서 컬렉션을 선택합니다.  
  
### 컬렉션 또는 리소스 경로 사용 = 리소스 경로  
 **리소스 경로**  
 리소스 경로를 입력합니다. 예: Employees  
  
## 관련 항목:  
 [OData 원본 편집기&#40;열 페이지&#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)   
 [OData 원본 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)   
 [OData 연결 관리자](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  