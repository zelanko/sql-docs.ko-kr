---
title: XML 파일로 정책 기반 관리 패싯 상태 복사 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, copy facet state to XML file
ms.assetid: 7d604ab1-6dd6-4f8e-a79c-eba99ab106fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3cae39c440c86348763b20ae04c70b3ce2ecc181
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62667361"
---
# <a name="copy-a-policy-based-management-facet-state-to-an-xml-file"></a>XML 파일로 정책 기반 관리 패싯 상태 복사
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 패싯의 상태를 XML 파일에 복사하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 패싯 상태를 XML 파일에 복사하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 이 항목의 절차를 수행하려면 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-copy-a-facet-state-to-an-xml-file"></a>패싯 상태를 XML 파일에 복사하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스, 인스턴스 개체, 데이터베이스 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭한 다음 **패싯**을 클릭합니다.  
  
2.  **패싯 보기 –** _object_name_ 대화 상자에서 **정책으로 현재 상태 내보내기**를 클릭합니다.  
  
3.  **정책으로 내보내기** 대화 상자에서 파일의 경로와 이름을 입력하거나 찾아보기( **...** ) 단추를 사용하여 파일을 찾은 다음 XML 파일의 이름을 입력합니다. 이 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [Export As Policy Dialog Box](export-as-policy-dialog-box.md)를 참조하세요.  
  
4.  완료되었으면 **확인**을 클릭합니다.  
  
  
