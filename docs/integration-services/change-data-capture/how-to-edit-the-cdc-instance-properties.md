---
description: CDC 인스턴스 속성을 편집하는 방법
title: CDC 인스턴스 속성을 편집하는 방법 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ee2861b40dbe132e7c95b52802bd10ccd46c20c1
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88426095"
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>CDC 인스턴스 속성을 편집하는 방법

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  이 절차에서는 CDC Designer 콘솔을 사용하여 CDC 인스턴스에 대한 구성 속성을 편집하는 방법에 대해 설명합니다.  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>CDC 인스턴스 구성 속성을 편집하려면  
  
1.  **시작** 메뉴에서 **CDC Designer 콘솔** 을 선택합니다.  
  
2.  왼쪽 창에서 **변경 데이터 캡처** 를 확장한 다음 편집할 속성을 가진 인스턴스를 포함하는 서비스를 확장합니다.  
  
3.  속성을 편집할 인스턴스의 이름을 선택합니다.  
  
4.  CDC Designer 콘솔의 오른쪽에 있는 동작 창에서 **속성** 을 클릭합니다.  
  
     속성을 편집할 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성** 을 클릭할 수도 있습니다.  
  
5.  속성 편집기의 다음 탭에서 속성을 편집합니다.  
  
    -   **Oracle**: U속성 편집기에서 **Oracle** 탭을 사용하여 새 인스턴스 마법사의 CDC 데이터베이스 만들기 페이지에 제공한 설명을 변경하고 Oracle 로그 마이닝 데이터베이스 연결 정보를 변경할 수 있습니다.  
  
         이 탭에서 편집할 수 있는 항목에 대한 자세한 내용은 [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md)을 참조하십시오.  
  
    -   **테이블**: **테이블** 탭을 사용하여 Oracle 원본 데이터베이스에서 선택한 테이블과 열을 변경할 수 있습니다.  
  
         이 탭에서 편집할 수 있는 항목에 대한 자세한 내용은 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)을 참조하십시오.  
  
    -   **스크립트**: **스크립트** 탭을 사용하여 보완 로깅을 설정할 Oracle 원본 데이터베이스에서 스크립트를 실행하거나 다시 실행할 수 있습니다.  
  
         이 탭에서 수행할 수 있는 작업에 대한 자세한 내용은 [Review and Generate Supplemental Logging Scripts](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)을 참조하십시오.  
  
    -   **고급**: **고급** 탭을 사용하여 CDC 인스턴스에 특별 속성을 추가할 수 있습니다.  
  
         이 탭에서 수행할 수 있는 작업에 대한 자세한 내용은 [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md)을 참조하십시오.  
  
  
