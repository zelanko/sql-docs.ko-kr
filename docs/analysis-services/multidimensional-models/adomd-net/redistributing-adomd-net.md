---
title: "ADOMD.NET 재배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6587a23e479522453feb01bf7190cebc9fb505df
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="redistributing-adomdnet"></a>ADOMD.NET 재배포
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]ADOMD.NET을 사용 하는 응용 프로그램을 작성 하는 경우 응용 프로그램과 함께 적합 한 버전의 ADOMD.NET 재배포 해야 합니다. ADOMD.NET을 재배포하려면 ADOMD.NET 설치 프로그램을 응용 프로그램의 설치 프로그램에 포함합니다.  
  
 ADOMD.NET 설치 프로그램뿐만 아니라 최신 버전의 ADOMD.NET은 SQL Server 기능 팩의 일부로 Microsoft 다운로드 센터에 있습니다.  
  
 ADOMD.NET 설치 프로그램에서는 ADOMD.NET 파일을 설치 \< *시스템 드라이브*>: \Program Files\Microsoft.NET\ADOMD.NET\\*버전 번호*합니다.  
  
 ADOMD.NET 설치 프로그램을 포함한 후 응용 프로그램의 설치 프로그램을 통해 ADOMD.NET 설치 프로그램을 시작하고 ADOMD.NET을 설치합니다. 또한 사용자 환경에 따라 SQL Server가 관련 어셈블리를 신뢰할 수 있는지 확인해야 할 수 있습니다.  
  
 자세한 내용은 다음을 참조하세요.  
  
 [Microsoft SQL Server 용 기능 팩](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: ADOMD.NET 종속성](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>관련 항목:  
 [ADOMD.NET 클라이언트 프로그래밍](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [ADOMD.NET 서버 프로그래밍](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
