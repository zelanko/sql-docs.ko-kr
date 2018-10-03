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
manager: craigg
ms.openlocfilehash: 448eda8c3c77f410bedd88d1193f2302c926ee95
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681371"
---
# <a name="ado-fundamentals"></a>ADO 기본 사항
ADO는 프로그래밍 방식으로 액세스, 편집 및 다양 한 OLE DB 시스템 인터페이스를 통해 데이터 원본에서 데이터 업데이트에 대 한 개발자에 게 강력 하 고 논리 개체 모델을 제공 합니다. ADO의 가장 일반적인 사용법은 테이블 또는 테이블에서 관계형 데이터베이스를 쿼리, 검색, 응용 프로그램에서 결과 표시 및 아마도 수 하 고 데이터 변경 내용을 저장 하는 것입니다. 다른 작업은 다음과 같습니다.  
  
-   SQL을 사용 하 고 결과 표시 하는 데이터베이스를 쿼리 합니다.  
  
-   인터넷을 통해 파일 저장소에 액세스 정보입니다.  
  
-   전자 메일 시스템에서 메시지 및 폴더를 조작 합니다.  
  
-   데이터베이스에서 데이터를 XML 파일로 저장합니다.  
  
-   XML을 사용 하 여 설명 하는 명령을 실행 하 고 XML 스트림을 검색 합니다.  
  
-   이진 또는 XML 스트림에서에 데이터를 저장합니다.  
  
-   사용자를를 검토 하 고 데이터베이스 테이블의 데이터를 변경할 수 있습니다.  
  
-   매개 변수가 있는 데이터베이스 명령 만들기 및 다시 사용  
  
-   저장된 프로시저를 실행 합니다.  
  
-   동적으로 라고 하는 유연한 구조를 만들기는 **레코드 집합**저장, 탐색 및 데이터를 조작로 합니다.  
  
-   트랜잭션 데이터베이스 작업을 수행 합니다.  
  
-   필터링 및 런타임 조건을 기반으로 하는 데이터베이스 정보의 로컬 복사본을 정렬 합니다.  
  
-   페이지를 만들고 데이터베이스에서 계층적 결과 조작 합니다.  
  
-   데이터 인식 구성 요소를 데이터베이스 필드를 바인딩합니다.  
  
-   연결이 끊긴 원격을 만들 **레코드 집합**합니다.  
  
 ADO는 이러한 유연성을 제공 하는 옵션 및 설정의 광범위 한을 노출 합니다. 따라서 체계적인 방법을 각 목표를 관리 가능한 부분으로 분할 응용 프로그램에서 ADO를 사용 하는 방법을 학습 하는 데 중요 한 것입니다.  
  
 ADO를 사용 하는 대부분의 응용 프로그램에 관련 된 네 가지 기본 작업: 데이터 가져오기, 데이터를 검사, 데이터, 편집 및 데이터를 업데이트 합니다. 이러한 작업은이 섹션의 뒷부분에 자세히 검사 합니다.  
  
 그러나 이러한 세부 정보를 이야기 하기 전에 살펴봅니다 ADO 개체 모델 및 간단한 ADO 응용 프로그램, Microsoft® Visual Basic®로 작성 되 고 각 네 가지 기본 ADO 작업을 수행 하는 개요를:  
  
-   [ADO 개체 및 컬렉션](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: 간단한 ADO 응용 프로그램](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [OLE DB 공급자](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [오류](../../../ado/guide/data/errors-ado.md)
