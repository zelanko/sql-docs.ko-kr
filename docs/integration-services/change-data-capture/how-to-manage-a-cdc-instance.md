---
title: CDC 인스턴스 관리 방법 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5d9e677f-b872-497d-9cde-472184a214ab
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5fd3788cb31e7e3e6408cc7161f45ba008cf081c
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728776"
---
# <a name="how-to-manage-a-cdc-instance"></a>How to Manage a CDC Instance

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  이 절차에서는 CDC Designer 콘솔을 사용하여 런타임에 CDC 인스턴스 작업을 관리하는 방법에 대해 설명합니다.  
  
### <a name="to-manage-cdc-instance-operations"></a>CDC 인스턴스 작업을 관리하려면  
  
1.  **시작** 메뉴에서 **CDC Designer 콘솔**을 선택합니다.  
  
2.  왼쪽 창에서 **변경 데이터 캡처** 를 확장한 다음 보려는 인스턴스를 포함하는 서비스를 확장합니다.  
  
3.  작업할 인스턴스의 이름을 선택합니다.  
  
4.  CDC Designer 콘솔의 오른쪽에 있는 **동작** 창에서 수행할 작업을 클릭합니다.  
  
     또한 왼쪽 창에서 인스턴스의 이름을 마우스 오른쪽 단추로 클릭하고 수행할 작업을 선택합니다.  
  
     다음 태스크를 수행할 수 있습니다.  
  
    -   **시작**: 변경 캡처를 시작합니다.  
  
    -   **중지**: 변경 캡처를 중지합니다.  
  
    -   **다시 설정**: **다시 설정** 을 클릭하여 CDC 인스턴스를 초기(비어 있음) 상태로 다시 설정합니다. 이 옵션은 CDC 인스턴스가 중지된 경우에 사용할 수 있습니다. 변경 테이블의 모든 변경 사항과 CDC 인스턴스 내부 상태가 삭제됩니다. CDC 인스턴스를 나중에 시작하면 변경 캡처가 해당 시점에서 시작되고 CDC 인스턴스가 시작된 후에 시작된 트랜잭션만 포함됩니다.  
  
    -   **삭제**: DAC 인스턴스를 삭제합니다.  
  
    -   **Oracle 로깅 스크립트**: **Oracle 로깅 스크립트**를 클릭하여 Oracle 로깅 스크립트 대화 상자를 Oracle 보완 로깅 스크립트와 함께 표시할 수 있습니다. 이 대화 상자에서 수행할 수 있는 작업에 대한 자세한 내용은 [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md)를 참조하십시오.  
  
         **참고**: 보완 로깅 스크립트를 실행하면 유효한 Oracle 사용자 이름과 암호를 입력할 수 있는 스크립트 실행을 위한 Oracle 자격 증명 대화 상자가 열립니다. 적절한 Oracle 자격 증명을 제공하는 방법은 [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)을 참조하십시오.  
  
    -   **CDC 인스턴스 배포**: CDC 인스턴스에 대한 배포 스크립트를 생성합니다. 이 대화 상자에 대한 자세한 내용은 [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md)를 참조하십시오.  
  
     위의 태스크에 대한 자세한 내용은 [Manage a CDC Instance](../../integration-services/change-data-capture/manage-a-cdc-instance.md)를 참조하십시오.  
  
 또한 **속성** 을 선택하여 CDC 인스턴스 구성 속성을 편집할 수 있습니다. CDC 인스턴스 속성을 편집하는 방법은 [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md)을 참조하십시오.  
  
  
