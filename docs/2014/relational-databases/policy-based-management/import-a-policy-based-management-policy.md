---
title: 정책 기반 관리 정책 가져오기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c8be774191f0ea5e637c157be7dc95d98929ec2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48175223"
---
# <a name="import-a-policy-based-management-policy"></a>정책 기반 관리 정책 가져오기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 정책 인스턴스를 가져오는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 정책 인스턴스를 가져오려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 모니터링하는 데 사용할 수 있는 정책과 함께 제공됩니다. 기본적으로 이러한 정책은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 설치되지 않지만 기본 위치인 C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1042에서 가져올 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-import-a-policy-instance"></a>정책 인스턴스를 가져오려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 새로 가져온 정책 인스턴스가 상주할 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  **정책** 폴더를 마우스 오른쪽 단추로 클릭하고 **정책 가져오기**를 선택합니다.  
  
5.  **가져오기** 대화 상자에서 파일의 경로와 이름을 입력하거나 찾아보기(**...**) 단추를 사용하여 정책이 포함된 XML 파일을 찾은 다음 파일을 선택합니다. **가져오기** 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [Import Policies Dialog Box](import-policies-dialog-box.md)를 참조하세요.  
  
6.  완료되었으면 **확인**을 클릭합니다.  
  
  
