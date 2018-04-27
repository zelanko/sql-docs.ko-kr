---
title: 프로그래밍 방식으로 패키지 저장 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: building-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b27925b4e1234c2c32b6070a733dae598727a5f2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="saving-a-package-programmatically"></a>프로그래밍 방식으로 패키지 저장
  프로그래밍 방식으로 새 패키지를 작성하거나 기존 패키지를 수정한 후에는 일반적으로 변경 내용을 저장합니다.  
  
 이 항목에서 설명하는 패키지 저장 방법을 사용할 경우에는 항상 **Microsoft.SqlServer.ManagedDTS** 어셈블리에 대한 참조가 필요합니다. 새 프로젝트에 참조를 추가한 후 **using** 또는 **Imports** 문을 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime> 네임스페이스를 가져옵니다.  
  
## <a name="saving-a-package-programmatically"></a>프로그래밍 방식으로 패키지 저장  
 프로그래밍 방식으로 패키지를 저장하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 다음 메서드 중 하나를 호출합니다.  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|파일|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> 로 구분하거나 여러<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 "." 또는 로컬 서버의 서버 이름만 지원합니다. "(local)" 또는 "localhost"는 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [패키지 저장](../../integration-services/save-packages.md)  
  
  
