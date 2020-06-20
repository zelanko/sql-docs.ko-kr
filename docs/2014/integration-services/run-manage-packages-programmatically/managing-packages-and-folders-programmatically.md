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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ae44d737f596b72dc535812a628740474f2a114f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964473"
---
# <a name="managing-packages-and-folders-programmatically"></a>프로그래밍 방식으로 패키지 및 폴더 관리
  프로그래밍 방식으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 대한 작업을 수행할 때 개별 패키지 또는 폴더가 있는지 여부를 확인하거나 패키지가 저장된 폴더를 관리할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스는 이 요구 사항을 충족하기 위한 다양한 메서드를 제공합니다.  
  
##  <a name="determining-whether-a-package-or-folder-exists"></a><a name="exists"></a> 패키지 또는 폴더가 있는지 확인  
 저장된 패키지가 있는지 여부를 프로그래밍 방식으로 확인하려면 해당 패키지를 로드 및 실행하기 전에 다음 메서드 중 하나를 호출합니다.  
  
|스토리지 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|  
  
 폴더가 있는지 여부를 프로그래밍 방식으로 확인하려면 해당 폴더에 저장된 패키지를 나열하기 전에 다음 메서드 중 하나를 호출합니다.  
  
|스토리지 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|  
  

  
##  <a name="managing-packages-and-folders"></a><a name="managing"></a> 패키지 및 폴더 관리  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스에서는 패키지와 패키지가 저장된 폴더를 관리하기 위한 추가 메서드를 제공합니다.  
  
###  <a name="removing-a-package"></a><a name="managing_rempkg"></a> 패키지 제거  
 저장된 패키지를 프로그래밍 방식으로 제거하려면 다음 메서드 중 하나를 호출합니다.  
  
|스토리지 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|  
  

  
###  <a name="creating-a-folder"></a><a name="managing_create"></a> 폴더 만들기  
 프로그래밍 방식으로 스토리지 폴더를 만들려면 다음 메서드 중 하나를 호출합니다.  
  
|스토리지 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|  
  

  
###  <a name="removing-a-folder"></a><a name="managing_remfldr"></a> 폴더 제거  
 프로그래밍 방식으로 스토리지 폴더를 제거하려면 다음 메서드 중 하나를 호출합니다.  
  
|스토리지 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|  
  
  
  
###  <a name="renaming-a-folder"></a><a name="managing_rename"></a> 폴더 이름 바꾸기  
 프로그래밍 방식으로 스토리지 폴더의 이름을 바꾸려면 다음 메서드 중 하나를 호출합니다.  
  
|스토리지 위치|호출할 메서드|  
|----------------------|--------------------|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|  
  

  
![Integration Services 아이콘 (작은 아이콘)](../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SSIS 서비스를 &#40;패키지 관리&#41;](../service/package-management-ssis-service.md)   
 [프로그래밍 방식으로 사용 가능 패키지 열거](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
