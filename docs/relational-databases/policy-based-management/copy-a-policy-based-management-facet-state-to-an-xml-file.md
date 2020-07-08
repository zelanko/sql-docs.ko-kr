---
title: 정책 기반 관리 패싯 상태를 XML 파일에 복사
description: SSMS(SQL Server Management Studio)를 사용하여 정책 기반 관리 패싯의 상태를 XML 파일에 복사하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, copy facet state to XML file
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 05235a6f2bc0ed2450e71397770599a5e22ea3d1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85654731"
---
# <a name="copy-a-policy-based-management-facet-state-to-an-xml-file"></a>XML 파일로 정책 기반 관리 패싯 상태 복사
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 패싯의 상태를 XML 파일에 복사하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 패싯 상태를 XML 파일에 복사하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 이 항목의 절차를 수행하려면 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-copy-a-facet-state-to-an-xml-file"></a>패싯 상태를 XML 파일에 복사하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스, 인스턴스 개체, 데이터베이스 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭한 다음 **패싯**을 클릭합니다.  
  
2.  **패싯 보기 –** _object_name_ 대화 상자에서 **정책으로 현재 상태 내보내기**를 클릭합니다.  
  
3.  **정책으로 내보내기** 대화 상자에서 파일의 경로와 이름을 입력하거나 찾아보기( **...** ) 단추를 사용하여 파일을 찾은 다음 XML 파일의 이름을 입력합니다. 이 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [Export As Policy Dialog Box](../../relational-databases/policy-based-management/export-as-policy-dialog-box.md)를 참조하세요.  
  
4.  완료되었으면 **확인**을 클릭합니다.  
  
  
