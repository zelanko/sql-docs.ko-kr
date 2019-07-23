---
title: 사용자 지정 보고서 실행 경고 표시 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 14d7372258e3cc15eb3da6d5577145b588473388
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262131"
---
# <a name="unsuppress-run-custom-report-warnings"></a>사용자 지정 보고서 실행 경고 표시
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
사용자 지정 보고서에 대한 경고 대화 상자에는 두 가지가 있습니다. 이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 이러한 상자를 표시하는 방법에 대해 설명합니다.  
  
기본적으로 사용자 지정 보고서가 실행되기 전에 **사용자 지정 보고서 실행** 대화 상자가 표시됩니다. **이 경고 메시지를 다시 표시 안 함** 확인란을 선택하면 이 대화 상자가 더 이상 표시되지 않습니다. 또한 사용자 지정 보고서를 연 다음 링크를 클릭하여 다른 사용자 지정 보고서를 열면 기본적으로 **사용자 지정 보고서 실행** 대화 상자가 표시됩니다. 이 대화 상자는 드릴스루 사용자 지정 보고서 파일에 대한 채우기 경로를 표시합니다. **이 경고 메시지를 다시 표시 안 함** 확인란을 선택하면 이 대화 상자가 더 이상 표시되지 않습니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>주 사용자 지정 보고서 경고 대화 상자를 표시하려면  
  
1.  \<*Server*>\\<*Share*>|\<*Drive*>\Documents and Settings\\<UserProfile>\Application Data\Microsoft\Microsoft SQL Server\130\Tools\Shell\reports.xml에 연결합니다.  
  
2.  **reports.xml**을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **<SuppressWarning>true\<\/SuppressWarning>을 <SuppressWarning>false\<\/SuppressWarning>** 으로 변경합니다.  
  
4.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 다시 시작합니다.  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>드릴스루 사용자 지정 보고서 경고 대화 상자를 표시하려면  
  
1.  \<*Server*>\\<*Share*>|\<*Drive*>\Documents and Settings\\<UserProfile>\Application Data\Microsoft\Microsoft SQL Server\130\Tools\Shell\reports.xml에 연결합니다.  
  
2.  **reports.xml**을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.  
  
3.  **<SuppressDrillthroughWarning>true\<\/SuppressDrillthroughWarning>을 <SuppressDrillthroughWarning>false\<\/SuppressDrillthroughWarning>** 으로 변경합니다.  
  
4.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 다시 시작합니다.  
  
## <a name="see-also"></a>참고 항목  
[Management Studio의 사용자 지정 보고서](../../ssms/object/custom-reports-in-management-studio.md)  
[Management Studio에 사용자 지정 보고서 추가](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[개체 탐색기 노드 속성과 함께 사용자 지정 보고서 사용](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  
