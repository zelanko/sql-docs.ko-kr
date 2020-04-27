---
title: 로컬 CDC Service를 관리하는 방법 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f9be649-cd93-40c1-bc48-0480106f207c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 27ec5fcac246c9907d38d8e0eff4e82befb0a04e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771309"
---
# <a name="how-to-manage-a-local-cdc-service"></a>로컬 CDC Service를 관리하는 방법
  이 절차에서는 CDC Service 구성 콘솔을 사용하여 특정 CDC Service를 관리하는 방법에 대해 설명합니다.  
  
### <a name="to-manage-a-specific-cdc-service"></a>특정 CDC Service를 관리 하려면  
  
1.  **시작** 메뉴에서 **Oracle CDC Service 구성**을 선택합니다.  
  
2.  CDC Service 구성 콘솔의 왼쪽 창에서 **로컬 CDC Service**를 확장합니다.  
  
3.  작업할 CDC Service를 선택합니다.  
  
     작업할 CDC Service를 마우스 오른쪽 단추로 클릭하고 원하는 동작을 선택할 수도 있습니다.  
  
     **OR**  
  
     CDC Service 구성 콘솔의 왼쪽 창에서 **로컬 CDC Service** 를 선택한 다음 CDC Service 구성 콘솔의 가운데 섹션에서 작업할 서비스를 선택합니다.  
  
     작업할 CDC Service를 마우스 오른쪽 단추로 클릭하고 원하는 동작을 선택할 수도 있습니다.  
  
4.  CDC서비스를 작업할 때 다음과 같은 태스크를 수행할 수 있습니다.  
  
    -   **서비스 삭제**  
  
         CDC Service 구성 콘솔 오른쪽의 **동작** 창에서 **삭제** 를 클릭하여 서비스를 삭제합니다.  
  
         삭제할 CDC Service를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택할 수도 있습니다.  
  
         **참고**: 서비스를 삭제할 때 서비스가 실행 중인 경우 서비스가 중지된 후에 삭제됩니다.  
  
         Oracle CDC Windows 서비스 정의를 삭제하려면 프로그램은 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 MSXDBCDC 데이터베이스에 대한 액세스 권한을 업데이트해야 합니다. **확인** 을 클릭하여 서비스를 삭제하면 프로그램은 MSXDBCDC 데이터베이스에서 Oracle CDC Service 등록을 삭제하려고 시도합니다. 권한 부족으로 인해 실패할 경우 사용자가 MSXDBCDC 데이터베이스의 업데이트 권한이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력할 수 있는 대화 상자가 표시됩니다.  
  
         SQL Server에 연결 대화 상자에 입력해야 하는 데이터에 대한 자세한 내용은 [Manage an Oracle CDC Service](manage-an-oracle-cdc-service.md) 및 [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md)을 참조하십시오.  
  
    -   **CDC Service 속성 편집**  
  
         CDC Service 구성 콘솔 오른쪽의 **동작** 창에서 **속성**을 클릭합니다.  
  
         속성을 편집할 CDC Service를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle CDC Service 관리](manage-an-oracle-cdc-service.md)  
  
  
