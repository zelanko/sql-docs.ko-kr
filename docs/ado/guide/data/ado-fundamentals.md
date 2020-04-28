---
title: ADO 기본 사항 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 75f5030f8faa5aa5d8e8a0f6bcb6d72b186c8448
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926068"
---
# <a name="ado-fundamentals"></a>ADO 기본 사항
ADO는 개발자에 게 OLE DB 시스템 인터페이스를 통해 다양 한 데이터 소스의 데이터를 프로그래밍 방식으로 액세스, 편집 및 업데이트할 수 있는 강력한 논리 개체 모델을 제공 합니다. ADO의 가장 일반적인 사용법은 관계형 데이터베이스의 테이블을 쿼리하고, 결과를 검색 하 여 응용 프로그램에 표시 하 고, 사용자가 데이터를 변경 하 고 변경 내용을 저장할 수 있도록 하는 것입니다. 다른 작업에는 다음이 포함 됩니다.  
  
-   SQL을 사용 하 여 데이터베이스를 쿼리하고 결과를 표시 합니다.  
  
-   인터넷을 통해 파일 저장소의 정보에 액세스 합니다.  
  
-   전자 메일 시스템에서 메시지 및 폴더 조작  
  
-   데이터베이스의 데이터를 XML 파일로 저장 합니다.  
  
-   XML로 설명 된 명령을 실행 하 고 XML 스트림을 검색 합니다.  
  
-   이진 또는 XML 스트림에 데이터 저장  
  
-   사용자가 데이터베이스 테이블의 데이터를 검토 하 고 변경할 수 있습니다.  
  
-   매개 변수가 있는 데이터베이스 명령 만들기 및 다시 사용  
  
-   저장 프로시저 실행  
  
-   데이터를 저장, 탐색 및 조작 하기 위해 **레코드 집합**이라는 유연한 유연한 구조를 동적으로 만듭니다.  
  
-   트랜잭션 데이터베이스 작업을 수행 합니다.  
  
-   런타임 조건에 따라 데이터베이스 정보의 로컬 복사본을 필터링 및 정렬 합니다.  
  
-   데이터베이스에서 계층적 결과 만들기 및 조작  
  
-   데이터베이스 필드를 데이터 인식 구성 요소에 바인딩합니다.  
  
-   연결 되지 않은 원격 **레코드 집합**을 만듭니다.  
  
 ADO는 이러한 유연성을 제공 하기 위한 다양 한 옵션 및 설정을 제공 합니다. 따라서 응용 프로그램에서 ADO를 사용 하 여 각 목표를 관리 가능한 조각으로 세분화 하는 방법을 배우는 것이 중요 합니다.  
  
 ADO를 사용 하는 대부분의 응용 프로그램에는 데이터 가져오기, 데이터 검사, 데이터 편집, 데이터 업데이트와 같은 네 가지 기본 작업이 포함 됩니다. 이러한 작업은이 섹션의 뒷부분에서 좀 더 자세히 검토 합니다.  
  
 그러나 이러한 세부 정보를 설명 하기 전에 ADO 개체 모델 및 간단한 ADO 응용 프로그램에 대 한 개요를 제공 합니다 .이 응용 프로그램은 Microsoft® Visual Basic® 하 고 각각의 네 가지 기본 ADO 작업을 수행 합니다.  
  
-   [ADO 개체 및 컬렉션](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: 간단한 ADO 애플리케이션](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [OLE DB 공급자](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [오류](../../../ado/guide/data/errors-ado.md)
