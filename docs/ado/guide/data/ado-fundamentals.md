---
title: "ADO 기본 사항 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a6b693060ad00f8b18268c503a7d0a96f3e5e62a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="ado-fundamentals"></a>ADO 기본 사항
ADO 개발자는 강력 하 고 논리 개체 모델 프로그래밍 방식으로 액세스, 편집 및 다양 한 OLE DB 시스템 인터페이스를 통해 데이터 원본에서에서 데이터 업데이트를 제공 합니다. ADO의 가장 일반적인 사용법은 테이블 또는 관계형 데이터베이스 테이블에서에서 쿼리, 검색 및 응용 프로그램에 결과 표시 및 아마도 사용자가 확인 하 고 변경 된 데이터에 저장할 수 있도록 하는 것입니다. 다른 작업은 다음과 같습니다.  
  
-   SQL을 사용 하 고 결과 표시 하는 데이터베이스를 쿼리 합니다.  
  
-   인터넷을 통해 파일 저장소에 있는 정보에 액세스 합니다.  
  
-   전자 메일 시스템의 메시지와 폴더를 조작 합니다.  
  
-   XML 파일에는 데이터베이스에서 데이터를 저장 합니다.  
  
-   XML과 함께 설명 하는 명령을 실행 하 고 XML 스트림을 검색 합니다.  
  
-   XML 스트림 또는 이진 데이터를 저장 합니다.  
  
-   사용자를 검토 하 고 데이터베이스 테이블의 데이터를 변경할 수 있습니다.  
  
-   매개 변수가 있는 데이터베이스 명령 만들기 및 다시 사용  
  
-   저장된 프로시저를 실행 합니다.  
  
-   동적으로 이라고 하는 유연한 구조를 만들어는 **레코드 집합**를 보유, 탐색 및 데이터를 조작 합니다.  
  
-   트랜잭션 데이터베이스 작업을 수행 합니다.  
  
-   필터링 및 정렬 실행 시간 조건을 기반으로 하는 데이터베이스 정보의 로컬 복사본입니다.  
  
-   만들기 및 조작 계층적 데이터베이스에서 발생 합니다.  
  
-   데이터 인식 구성 요소를 데이터베이스 필드에 바인딩  
  
-   연결 되지 않은 원격 만들기, **레코드 집합**합니다.  
  
 ADO는 다양 한 이러한 유연성을 제공 하는 옵션 및 설정을 노출 합니다. 따라서이 체계적인 방법을 각 목표를 관리 가능한 부분으로 분할 응용 프로그램에서 ADO를 사용 하는 방법을 배우는 데 중요 합니다.  
  
 ADO를 사용 하는 대부분의 응용 프로그램의 네 가지 기본 작업이 포함 됩니다: 데이터 가져오기, 데이터를 검사, 데이터를 편집 및 데이터를 업데이트 합니다. 이러한 작업은이 섹션의 뒷부분에 보다 자세히 검사 합니다.  
  
 그러나 이러한 세부 정보를 논의하기 전에 ADO 개체 모델 및 Microsoft® Visual Basic®에서 기록 되 고 각각의 네 가지 기본 ADO 작업을 수행 하는 간단한 ADO 응용 프로그램을 개략적으로 제공할 것:  
  
-   [ADO 개체 및 컬렉션](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: 간단한 ADO 응용 프로그램](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [OLE DB 공급자](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [오류](../../../ado/guide/data/errors-ado.md)
