---
description: Manage an Oracle CDC Service
title: Oracle CDC Service 관리 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 5972cee3-b1a9-4c56-aed6-bdddf84af283
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aea4d1beb0a77e6bc7a0456c3f3437c919698bcd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426075"
---
# <a name="manage-an-oracle-cdc-service"></a>Manage an Oracle CDC Service

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  CDC Service 구성 콘솔을 사용하여 특정 CDC Service를 관리할 수 있습니다.  
  
 **작업할 CDC Service를 선택하려면**  
  
1.  CDC Service 구성 콘솔의 왼쪽 창에서 **로컬 CDC Service**를 확장합니다.  
  
2.  작업할 CDC Service를 선택합니다.  
  
     작업할 CDC Service를 마우스 오른쪽 단추로 클릭하고 원하는 동작을 선택할 수도 있습니다. [CDC Service에서 수행할 수 있는 작업](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md#BKMK_WhatcandowithCDCService)을 참조하세요.  
  
 **OR**  
  
1.  CDC Service 구성 콘솔의 왼쪽 창에서 **로컬 CDC Service** 를 선택합니다.  
  
2.  CDC Service 구성 콘솔의 가운데 섹션에서 작업할 서비스를 선택합니다.  
  
     작업할 CDC Service를 마우스 오른쪽 단추로 클릭하고 원하는 동작을 선택할 수도 있습니다. [CDC Service에서 수행할 수 있는 작업](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md#BKMK_WhatcandowithCDCService)을 참조하세요.  
  
##  <a name="what-can-you-do-with-a-cdc-service"></a><a name="BKMK_WhatcandowithCDCService"></a> CDC Service에서 수행할 수 있는 작업  
 CDC서비스에서 작업할 때 다음과 같은 동작을 수행할 수 있습니다.  
  
### <a name="delete-the-service"></a>서비스 삭제  
 CDC Service 구성 콘솔 오른쪽의 **동작** 창에서 **삭제** 를 클릭하여 서비스를 삭제합니다.  
  
 삭제할 CDC Service를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택할 수도 있습니다.  
  
 **참고**: 서비스를 삭제할 때 서비스가 실행 중인 경우 서비스가 중지된 후에 삭제됩니다.  
  
 Oracle CDC Windows 서비스 정의를 삭제하려면 프로그램은 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 MSXDBCDC 데이터베이스에 대한 액세스 권한을 업데이트해야 합니다. 확인을 클릭하여 서비스를 삭제하면 프로그램은 MSXDBCDC 데이터베이스에서 Oracle CDC Service 등록을 삭제하려고 시도합니다. 프로그램에 적절한 권한이 없기 때문에 Oracle CDC Service 등록을 삭제할 수 없는 경우 MSXDBCDC 데이터베이스에 대한 업데이트 권한이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력하라는 메시지가 사용자에게 표시됩니다.  
  
 SQL Server에 연결 대화 상자에 입력해야 하는 데이터에 대한 자세한 내용은 [Connection to SQL Server for Delete](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md)을 참조하십시오.  
  
### <a name="edit-the-cdc-service-properties"></a>CDC Service 속성 편집  
 CDC Service 구성 콘솔 오른쪽의 **동작** 창에서 **속성**을 클릭합니다.  
  
 속성을 편집할 CDC Service를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [로컬 CDC Service를 관리하는 방법](../../integration-services/change-data-capture/how-to-manage-a-local-cdc-service.md)  
  
  
