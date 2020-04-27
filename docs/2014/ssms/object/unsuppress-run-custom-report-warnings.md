---
title: 사용자 지정 보고서 실행 경고 표시 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed653b16fe524f364ba89f13e00715b725080033
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62824399"
---
# <a name="unsuppress-run-custom-report-warnings"></a>사용자 지정 보고서 실행 경고 표시
  사용자 지정 보고서에 대한 경고 대화 상자에는 두 가지가 있습니다. 이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 이러한 상자를 표시하는 방법에 대해 설명합니다.  
  
 기본적으로 사용자 지정 보고서가 실행되기 전에 **사용자 지정 보고서 실행** 대화 상자가 표시됩니다. **이 경고 메시지를 다시 표시 안 함** 확인란을 선택하면 이 대화 상자가 더 이상 표시되지 않습니다. 또한 사용자 지정 보고서를 연 다음 링크를 클릭하여 다른 사용자 지정 보고서를 열면 기본적으로 **사용자 지정 보고서 실행** 대화 상자가 표시됩니다. 이 대화 상자는 드릴스루 사용자 지정 보고서 파일에 대한 채우기 경로를 표시합니다. **이 경고 메시지를 다시 표시 안 함** 확인란을 선택하면 이 대화 상자가 더 이상 표시되지 않습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>주 사용자 지정 보고서 경고 대화 상자를 표시하려면  
  
1.  \< *서버*\<*Drive* *Share*\\ 공유 드라이브> \documents 및 설정<UserProfile\>\Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.에 연결 합니다.>|>\\<  
  
2.  를 마우스 오른쪽 `reports.xml`단추로 클릭 한 다음 **편집**을 클릭 합니다.  
  
3.  **\<SuppressWarning\<>true/SuppressWarning>를 SuppressWarning \<>false\</SuppressWarning>로 **변경 합니다.  
  
4.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 다시 시작합니다.  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>드릴스루 사용자 지정 보고서 경고 대화 상자를 표시하려면  
  
1.  \< *서버*\<*Drive* *Share*\\ 공유 드라이브> \documents 및 설정<UserProfile\>\Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.에 연결 합니다.>|>\\<  
  
2.  를 마우스 오른쪽 `reports.xml`단추로 클릭 하 고 **편집**을 클릭 합니다.  
  
3.  ** \<SuppressDrillthroughWarning\<>true/SuppressDrillthroughWarning>를 SuppressDrillthroughWarning \<>false\</SuppressDrillthroughWarning>로 **변경 합니다.  
  
4.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 다시 시작합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Management Studio의 사용자 지정 보고서](custom-reports-in-management-studio.md)   
 [Management Studio에 사용자 지정 보고서 추가](add-a-custom-report-to-management-studio.md)   
 [개체 탐색기 노드 속성과 함께 사용자 지정 보고서 사용](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
