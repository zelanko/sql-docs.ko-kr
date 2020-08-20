---
description: SQL Server Data Tools에서 패키지 복사
title: SQL Server Data Tools에서 패키지 복사 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9b1f57c7b37994a9a34a792fab2ab19169aa5d9e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457542"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>SQL Server Data Tools에서 패키지 복사

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  이 항목에서는 기존 패키지를 복사하여 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 만드는 방법과 새 패키지의 **Name** 및 **GUID** 속성을 업데이트하는 방법에 대해 설명합니다.  
  
### <a name="to-copy-a-package"></a>패키지를 복사하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 복사할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭합니다.  
  
3.  복사할 패키지를 솔루션 탐색기에서 선택했는지 또는 패키지가 포함된 SSIS 디자이너의 탭이 활성 상태인지 확인합니다.  
  
4.  **파일** 메뉴에서 **다른 이름으로 \<package name> 저장**을 클릭합니다.  
  
    > [!NOTE]  
    >  SSIS 디자이너에서 패키지를 열어야 **파일** 메뉴에 **다른 이름으로 저장** 옵션이 표시됩니다.  
  
5.  필요에 따라 다른 폴더를 찾습니다.  
  
6.  패키지 파일 이름을 업데이트합니다. .dtsx 파일 확장명을 유지해야 합니다.  
  
7.  **저장**을 클릭합니다.  
  
8.  프롬프트에서 파일 이름과 일치시킬 패키지 개체의 이름을 업데이트할 것인지 여부를 선택합니다. **예**를 클릭하면 패키지의 **Name** 속성이 업데이트됩니다. 새 패키지가 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 추가되고 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 열립니다.  
  
9. 필요에 따라 **제어 흐름** 탭의 배경을 클릭하고 **속성**을 클릭합니다.  
  
10. 속성 창에서 ID 속성 값을 클릭한 다음, 드롭다운 목록에서 **\<Generate New ID>** 를 클릭합니다.  
  
11. **파일** 메뉴에서 **선택한 항목 저장** 을 클릭하여 새 패키지를 저장합니다.  
  
## <a name="see-also"></a>참고 항목  
 [패키지의 복사본 저장](https://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [SQL Server Data Tools에서 패키지 만들기](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integration Services&#40;SSIS&#41; 패키지](../integration-services/integration-services-ssis-packages.md)  
  
  
