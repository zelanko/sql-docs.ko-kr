---
title: Analysis Services 구성-데이터 디렉터리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ef732855-b7af-4f40-a619-5573c1c354bb
author: heidisteen
ms.author: heidist
ms.openlocfilehash: b31000d7d044a781b38faa7c366c8f8f6a439399
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045590"
---
# <a name="analysis-services-configuration---data-directories"></a>Analysis Services 구성 - 데이터 디렉터리
  다음 표의 기본 디렉터리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있습니다. 이러한 파일에 대 한 액세스 권한은 설치 중에 만들어지고 프로 비전 되는 SQLServerMSASUser $ 보안 그룹의 멤버와 로컬 관리자에 게 부여 됩니다 \<instance> .  
  
## <a name="ui-element-list"></a>UI 요소 목록  
  
|Description|기본 디렉터리|권장 사항|  
|-----------------|-----------------------|---------------------|  
|데이터 루트 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID> \OLAP\Data \| files\Microsoft SQL Server \ 폴더가 제한 된 권한으로 보호 되는지 확인 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 성능은 대부분의 구성에서 데이터 디렉터리가 있는 스토리지의 성능에 따라 달라집니다. 이 디렉터리는 시스템에 연결된 성능이 가장 높은 스토리지에 두십시오. 장애 조치(Failover) 클러스터 설치의 경우 공유 디스크에 데이터 디렉터리를 만들어야 합니다.|  
|로그 파일 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID> \OLAP\Log \| 로그 파일에 대 한 디렉터리 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이며 디렉터리 이며 flightrecorder 로그를 포함 합니다. 비행 레코더 기간을 늘려야 하는 경우 로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|임시 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID> \OLAP\Temp \| 는 고성능 저장소 하위 시스템에 임시 디렉터리를 저장 합니다.|  
|백업 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID> \OLAP\Backup \| 이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 백업 파일의 디렉터리입니다. SharePoint용 PowerPivot 설치 시에는 PowerPivot 시스템 서비스에서 PowerPivot 데이터 파일도 캐시합니다.<br /><br /> 데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스를 위한 사용자 그룹에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
## <a name="notes"></a>메모  
  
-   SharePoint 팜에 배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 애플리케이션 파일, 데이터 파일 및 속성을 콘텐츠 데이터베이스와 서비스 애플리케이션 데이터베이스에 저장합니다.  
  
-   기존 설치에 기능을 추가할 경우 이전에 설치한 기능의 위치를 변경하거나 새 기능의 위치를 지정할 수 없습니다.  
  
-   기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소도 별도의 디렉터리에 설치해야 합니다.  
  
-   다음과 같은 위치에는 프로그램 파일 및 데이터 파일을 설치할 수 없습니다.  
  
    -   이동식 디스크 드라이브  
  
    -   압축 파일 시스템  
  
    -   시스템 파일이 있는 디렉터리  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
  
