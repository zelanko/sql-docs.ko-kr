---
title: 프로그래밍 방식으로 패키지 저장 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 373240a3c693494c57f92c56cf9fd424bf87ae57
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37199743"
---
# <a name="saving-a-package-programmatically"></a>프로그래밍 방식으로 패키지 저장
  프로그래밍 방식으로 새 패키지를 작성하거나 기존 패키지를 수정한 후에는 일반적으로 변경 내용을 저장합니다.  
  
 이 항목에서 설명하는 패키지 저장 방법을 사용할 경우에는 항상 `Microsoft.SqlServer.ManagedDTS` 어셈블리에 대한 참조가 필요합니다. 새 프로젝트에 참조를 추가한 후 `using` 또는 `Imports` 문을 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime> 네임스페이스를 가져오십시오.  
  
## <a name="saving-a-package-programmatically"></a>프로그래밍 방식으로 패키지 저장  
 프로그래밍 방식으로 패키지를 저장하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 다음 메서드 중 하나를 호출합니다.  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|파일|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> 로 구분하거나 여러<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 "." 또는 로컬 서버의 서버 이름만 지원합니다. "(local)" 또는 "localhost"는 사용할 수 없습니다.  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정** <br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 저장](../save-packages.md)  
  
  
