---
title: 설치 역할 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c7e9db15-89f2-4d4d-8860-1e64c5821c4d
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: b1cf8c6f8442fc69669c10106f671040733e48ef
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092227"
---
# <a name="setup-role"></a>설치 역할
  이 페이지를 통해 기능 선택 페이지를 사용하여 개별 기능을 선택할지 설치 역할을 사용하여 설치할지 지정할 수 있습니다.  
  
 `setup role`은 미리 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성을 구현하는 데 필요한 모든 기능 및 공유 구성 요소의 고정된 선택 항목입니다.  
  
## <a name="options"></a>변수  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 설치**  
 이 옵션을 선택하여 개별 기능과 공유 구성 요소를 선택할 수 있습니다. 인스턴스 기능에는 데이터베이스 엔진 서비스, Analysis Services(기본 모드) 및 Reporting Services가 포함됩니다.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SharePoint 용 PowerPivot**  
 이 옵션을 선택하여 SharePoint 2010 팜에 Analysis Services 서버 구성 요소를 설치할 수 있습니다. 이 옵션은 팜에 PowerPivot 시스템 서비스와 Analysis Services 서버를 배포하여, 포함된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터가 들어 있는 게시된 Excel 통합 문서에 대해 쿼리 및 데이터 처리가 가능하도록 합니다.  
  
 SharePoint 팜에서 데이터베이스를 호스팅해야 하는 경우 필요에 따라 설치에 관계형 데이터베이스 엔진 인스턴스를 추가할 수 있습니다. 팜이 이미 구성되어 있는 경우 이 옵션을 건너뛸 수 있습니다.  
  
 설치가 완료 된 후 다음 방법 중 하나를 사용 하 여 소프트웨어를 구성 해야 합니다. PowerPivot 구성 도구, PowerShell cmdlet 또는 SharePoint 2010 중앙 관리 합니다. 이전 릴리스와 달리 설치 프로그램에서는 더 이상 PowerPivot 설치에 대한 구성 작업을 수행하지 않습니다.  
  
 역할 기반 설치에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot for Excel 클라이언트 응용 프로그램이 포함되어 있지 않습니다. 클라이언트 애플리케이션은 별도로 설치됩니다.  
  
 **모든 기능을 기본값으로 설치**  
 이 설치 역할을 선택하여 이번 릴리스에 사용할 수 있는 모든 기능을 설치할 수 있습니다. SharePoint용 PowerPivot은 이 역할에서 제외됩니다. 이 기능을 설치하려면 SharePoint용 PowerPivot 설치 역할을 사용해야 합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 **NT AUTHORITY\NETWORK SERVICE** 계정을 사용하여 시작되도록 구성됩니다. 현재 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**sysadmin** 역할의 멤버로 프로비전됩니다. 이 옵션으로 설정한 값은 추가 명령줄 매개 변수를 지정하여 재정의할 수 있습니다.  
  
 운영 체제가 도메인 컨트롤러가 아닌 경우, 기본적으로 데이터베이스 엔진 및 Reporting Services는 NTAUTHORITY\NETWORK SERVICE 계정을 사용하고 Integration Services는 NTAUTHORITY\NETWORK SERVICE 계정을 사용하고 SQL 전체 텍스트 필터 데몬 시작 관리자는 NTAUTHORITY\LOCAL SERVICE 계정을 사용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 용 PowerPivot 설치](https://go.microsoft.com/fwlink/?LinkId=206906)   
 [하드웨어 및 소프트웨어 요구 사항 (SharePoint 용 PowerPivot](https://go.microsoft.com/fwlink/?LinkId=216823)   
 [기능 선택](../../../2014/sql-server/install/feature-selection.md)  
  
  
