---
title: CDC 인스턴스 속성을 보는 방법 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4bce9b82-7bbd-41df-b3f4-4b40b8bad474
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eaf4308f05b7a7fb1f450947754736d0cf565b61
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294669"
---
# <a name="how-to-view-the-cdc-instance-properties"></a>CDC 인스턴스 속성을 보는 방법

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  이 절차에서는 CDC Designer 콘솔을 사용하여 인스턴스 작업을 쉽게 관리하기 위해 만든 인스턴스에 대한 정보를 보는 방법에 대해 설명합니다.  
  
### <a name="to-view-information-about-a-specific-instance"></a>특정 인스턴스에 대한 정보를 보려면  
  
1.  **시작** 메뉴에서 **CDC Designer 콘솔**을 선택합니다.  
  
2.  왼쪽 창에서 **변경 데이터 캡처** 를 확장한 다음 보려는 인스턴스를 포함하는 서비스를 확장합니다.  
  
3.  작업할 인스턴스의 이름을 선택합니다.  
  
     인스턴스에 대한 정보는 CDC Designer 콘솔의 가운데 부분에 표시됩니다. 또한 4개의 탭으로 구분됩니다. 모든 탭은 읽기 전용입니다.  
  
     **상태**  
     이 탭에는 인스턴스에 대한 변경 데이터 캡처의 현재 상태에 대한 정보가 표시됩니다. 이 탭에 표시되는 내용에 대한 자세한 내용은 **Manage a CDC Instance** 에서 [뷰어 탭](../../integration-services/change-data-capture/manage-a-cdc-instance.md)섹션을 참조하십시오.  
  
     **Oracle**  
     이 탭에는 CDC 인스턴스 및 Oracle 원본 데이터베이스에 대한 일반 정보가 표시됩니다. 이 탭에 표시되는 내용에 대한 자세한 내용은 [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md)을 참조하십시오.  
  
     **테이블**  
     이 탭에는 변경 데이터 캡처에 포함된 테이블에 대한 정보가 표시됩니다. 또한 캡처되는 열이 나열됩니다. 이 탭에 표시되는 내용에 대한 자세한 내용은 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)을 참조하십시오.  
  
     **고급**  
     이 탭에는 속성 편집기에서 정의하는 고급 속성 목록이 표시됩니다. 이 탭에 표시되는 내용에 대한 자세한 내용은 [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md)을 참조하십시오.  
  
  
