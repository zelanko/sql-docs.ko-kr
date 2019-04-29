---
title: Oracle CDC Service 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 5972cee3-b1a9-4c56-aed6-bdddf84af283
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9f9969630f8fe9f665a04575af8670ddb1af1b3c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62835636"
---
# <a name="manage-an-oracle-cdc-service"></a>Manage an Oracle CDC Service
  CDC Service 구성 콘솔을 사용하여 특정 CDC Service를 관리할 수 있습니다.  
  
 **작업할 CDC Service를 선택하려면**  
  
1.  CDC Service 구성 콘솔의 왼쪽 창에서 **로컬 CDC Service**를 확장합니다.  
  
2.  작업할 CDC Service를 선택합니다.  
  
     작업할 CDC Service를 마우스 오른쪽 단추로 클릭하고 원하는 동작을 선택할 수도 있습니다. [CDC Service에서 수행할 수 있는 작업](manage-an-oracle-cdc-service.md#BKMK_WhatcandowithCDCService)을 참조하세요.  
  
 **OR**  
  
1.  CDC Service 구성 콘솔의 왼쪽 창에서 **로컬 CDC Service** 를 선택합니다.  
  
2.  CDC Service 구성 콘솔의 가운데 섹션에서 작업할 서비스를 선택합니다.  
  
     작업할 CDC Service를 마우스 오른쪽 단추로 클릭하고 원하는 동작을 선택할 수도 있습니다. [CDC Service에서 수행할 수 있는 작업](manage-an-oracle-cdc-service.md#BKMK_WhatcandowithCDCService)을 참조하세요.  
  
##  <a name="BKMK_WhatcandowithCDCService"></a> CDC Service에서 수행할 수 있는 작업  
 CDC서비스에서 작업할 때 다음과 같은 동작을 수행할 수 있습니다.  
  
### <a name="delete-the-service"></a>서비스 삭제  
 CDC Service 구성 콘솔 오른쪽의 **동작** 창에서 **삭제** 를 클릭하여 서비스를 삭제합니다.  
  
 삭제할 CDC Service를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택할 수도 있습니다.  
  
 **참고**: 서비스를 삭제 하는 경우는 서비스가 실행 되 고, 서비스 삭제 되기 전에 중지 됩니다.  
  
 Oracle CDC Windows 서비스 정의를 삭제하려면 프로그램은 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 MSXDBCDC 데이터베이스에 대한 액세스 권한을 업데이트해야 합니다. 확인을 클릭하여 서비스를 삭제하면 프로그램은 MSXDBCDC 데이터베이스에서 Oracle CDC Service 등록을 삭제하려고 시도합니다. 프로그램에 적절한 권한이 없기 때문에 Oracle CDC Service 등록을 삭제할 수 없는 경우 MSXDBCDC 데이터베이스에 대한 업데이트 권한이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력하라는 메시지가 사용자에게 표시됩니다.  
  
 SQL Server에 연결 대화 상자에 입력해야 하는 데이터에 대한 자세한 내용은 [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md)을 참조하십시오.  
  
### <a name="edit-the-cdc-service-properties"></a>CDC Service 속성 편집  
 CDC Service 구성 콘솔 오른쪽의 **동작** 창에서 **속성**을 클릭합니다.  
  
 속성을 편집할 CDC Service를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [로컬 CDC Service를 관리하는 방법](how-to-manage-a-local-cdc-service.md)  
