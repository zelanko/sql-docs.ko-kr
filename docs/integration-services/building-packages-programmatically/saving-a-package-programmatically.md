---
title: "프로그래밍 방식으로 패키지 저장 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: f6b99377f6eaf720b9511b560e5cf563ede2b869
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="saving-a-package-programmatically"></a>프로그래밍 방식으로 패키지 저장
  프로그래밍 방식으로 새 패키지를 작성하거나 기존 패키지를 수정한 후에는 일반적으로 변경 내용을 저장합니다.  
  
 이 항목에서 설명하는 패키지 저장 방법을 사용할 경우에는 항상 **Microsoft.SqlServer.ManagedDTS** 어셈블리에 대한 참조가 필요합니다. 새 프로젝트에 대 한 참조를 추가한 후에 가져올는 <xref:Microsoft.SqlServer.Dts.Runtime> 포함 된 네임 스페이스는 **를 사용 하 여** 또는 **Imports** 문.  
  
## <a name="saving-a-package-programmatically"></a>프로그래밍 방식으로 패키지 저장  
 패키지를 프로그래밍 방식으로 저장 하려면 호출의 다음 메서드 중 하나는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스:  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|파일|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> 또는<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 "." 또는 로컬 서버의 서버 이름만 지원합니다. "(local)" 또는 "localhost"는 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [패키지 저장](../../integration-services/save-packages.md)  
  
  

