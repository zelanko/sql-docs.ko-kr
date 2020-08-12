---
title: Master Data Services 제거 | Microsoft 문서
description: 이 제거 프로세스는 로컬 컴퓨터에서 MDS(Master Data Services) 폴더 및 파일을 제거하고 Master Data Services 구성 관리자를 제거합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: efc2431c-588b-42e7-b23b-c875145a33f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec6345d4470c95669b13a08bde103057409bde67
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883722"
---
# <a name="uninstall-and-remove-master-data-services"></a>Master Data Services 제거
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 기능을 제거하려면 [SQL Server의 기존 인스턴스 제거&#40;설치 프로그램&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)의 단계를 따르고 **기능 선택** 페이지에서 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 제거할 기능으로 지정합니다. 제거 프로세스는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 폴더와 파일을 제거하고 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 를 로컬 컴퓨터에서 제거합니다.  
  
 데이터 손실을 방지하고 시스템의 다른 컴퓨터에 영향을 주지 않기 위해 일부 항목은 제거 프로세스에서 제거 또는 변경되지 않습니다. 다음 표를 검토하여 항목을 남겨둘지, 아니면 제거할지 여부를 결정합니다.  
  
|항목|설명|  
|----------|-----------------|  
|폴더 및 파일|제거 프로세스는 대부분의 폴더와 파일을 제거 경로에서 제거합니다.<br /><br /> 제거 프로세스는 설치 위치에서 Master Data Services 및 MDSTempDir 폴더를 제거하지 않습니다. 제거 프로세스가 완료된 후 이러한 폴더를 파일 시스템에서 수동으로 삭제할 수 있습니다. 자세한 내용은 [폴더 및 파일 사용 권한&#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)을 참조하세요.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 어셈블리|제거 프로세스는 GAC(전역 어셈블리 캐시)에서 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 어셈블리를 제거합니다.|  
|데이터베이스|제거 프로세스는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 영향을 주지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에서 데이터베이스는 그대로 유지되므로 마스터 데이터, 모델 개체, 사용자 및 그룹 권한, 비즈니스 규칙 등을 비롯한 어떠한 데이터도 손실되지 않습니다.<br /><br /> 데이터베이스가 필요하지 않고 이후에 다른 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 사이트나 애플리케이션에 연결할 계획이 없는 경우 데이터베이스를 호스팅하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 데이터베이스를 삭제할 수 있습니다. 자세한 내용은 [데이터베이스 삭제](../../relational-databases/databases/delete-a-database.md)를 참조하세요.|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 및 Web.config|제거 프로세스는 파일 시스템에서 WebApplication 폴더를 제거합니다. WebApplication 폴더에는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]용 웹 애플리케이션 파일과 Web.config 파일이 포함되어 있습니다.<br /><br /> **\*\* 중요 \*\*** 제거하기 전에 파일의 사용자 지정 설정 또는 기타 정보를 유지하기 위해 Web.config 파일을 다른 위치에 복사할 수 있습니다. 제거 프로세스가 완료된 후에는 Web.config 파일을 복구할 수 없습니다.|  
|인터넷 정보 서비스(IIS) 항목|제거 프로세스는 로컬 컴퓨터에 있는 IIS의 애플리케이션 풀, 웹 사이트 또는 웹 애플리케이션에 영향을 주지 않습니다. 제거 프로세스가 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]용 WebApplication 폴더 및 Web.config 파일을 제거하므로 이러한 파일이 필요한 모든 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션은 더 이상 콘텐츠를 서비스하지 않습니다. 사용자가 웹 애플리케이션에 액세스하려고 하면 HTTP 오류 500.19-내부 서버 오류: "요청된 페이지와 관련된 구성 데이터가 잘못되어 해당 페이지에 액세스할 수 없습니다."라는 오류가 발생합니다.<br /><br /> 웹 사이트 또는 애플리케이션 그리고 해당 사이트 또는 애플리케이션을 서비스하는 애플리케이션 풀이 더 이상 필요하지 않은 경우 IIS 도구를 사용하여 삭제할 수 있습니다. 자세한 내용은 [TechNet에서](https://go.microsoft.com/fwlink/?LinkId=184885) IIS 7.0: 작업 가이드 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 참조하십시오.|  
|**MDS_ServiceAccounts** 그룹|제거 프로세스가 완료된 후 **MDS_ServiceAccounts** Windows 그룹 및 이 그룹에 추가된 모든 서비스 계정은 남아 있습니다. 이 그룹과 계정이 더 이상 필요하지 않은 경우 제거할 수 있습니다.|  
|레지스트리|제거 프로세스에서는 Windows 레지스트리의 모든 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 레지스트리 키를 제거합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
