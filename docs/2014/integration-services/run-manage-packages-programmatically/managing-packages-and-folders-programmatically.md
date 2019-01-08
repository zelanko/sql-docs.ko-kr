---
title: 프로그래밍 방식으로 패키지 및 폴더 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c41f5d59b440fe7b72153076fac5bf794ab6420e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362136"
---
# <a name="managing-packages-and-folders-programmatically"></a>프로그래밍 방식으로 패키지 및 폴더 관리
  프로그래밍 방식으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 대한 작업을 수행할 때 개별 패키지 또는 폴더가 있는지 여부를 확인하거나 패키지가 저장된 폴더를 관리할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스는 이 요구 사항을 충족하기 위한 다양한 메서드를 제공합니다.  
  
##  <a name="exists"></a> 패키지 또는 폴더가 있는지 확인  
 저장된 패키지가 있는지 여부를 프로그래밍 방식으로 확인하려면 해당 패키지를 로드 및 실행하기 전에 다음 메서드 중 하나를 호출합니다.  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|  
  
 폴더가 있는지 여부를 프로그래밍 방식으로 확인하려면 해당 폴더에 저장된 패키지를 나열하기 전에 다음 메서드 중 하나를 호출합니다.  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|  
  

  
##  <a name="managing"></a> 패키지 및 폴더 관리  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스에서는 패키지와 패키지가 저장된 폴더를 관리하기 위한 추가 메서드를 제공합니다.  
  
###  <a name="managing_rempkg"></a> 패키지 제거  
 저장된 패키지를 프로그래밍 방식으로 제거하려면 다음 메서드 중 하나를 호출합니다.  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|  
  

  
###  <a name="managing_create"></a> 폴더 만들기  
 프로그래밍 방식으로 저장소 폴더를 만들려면 다음 메서드 중 하나를 호출합니다.  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|  
  

  
###  <a name="managing_remfldr"></a> 폴더 제거  
 프로그래밍 방식으로 저장소 폴더를 제거하려면 다음 메서드 중 하나를 호출합니다.  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|  
  
  
  
###  <a name="managing_rename"></a> 폴더 이름 바꾸기  
 프로그래밍 방식으로 저장소 폴더의 이름을 바꾸려면 다음 메서드 중 하나를 호출합니다.  
  
|저장소 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|  
  

  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 관리&#40;SSIS 서비스&#41;](../service/package-management-ssis-service.md)   
 [프로그래밍 방식으로 사용 가능 패키지 열거](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
