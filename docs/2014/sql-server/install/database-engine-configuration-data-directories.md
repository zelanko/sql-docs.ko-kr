---
title: 데이터베이스 엔진 구성-데이터 디렉터리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 9b1fa0fc-623b-479a-afc3-4f13bd850487
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b223c3ef9c6b4a8085c6575f827ae5e9e276ad9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992321"
---
# <a name="database-engine-configuration---data-directories"></a>데이터베이스 엔진 구성 - 데이터 디렉터리
  이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로그램 및 데이터 파일의 설치 위치를 지정할 수 있습니다. 설치 유형에 따라 지원되는 스토리지에 로컬 디스크, 공유 스토리지 또는 SMB 파일 서버가 포함될 수 있습니다.  
  
 SMB 파일 공유를 디렉터리로 지정하려면 지원되는 UNC 경로를 수동으로 입력해야 합니다. SMB 파일 공유를 찾아볼 수는 없습니다. SMB 파일 공유에 지원되는 UNC 경로 형식은 \\\Servername\ShareName\\....입니다.  
  
## <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 독립 실행형 인스턴스에 대한 지원되는 스토리지 유형 및 기본 디렉터리를 보여 줍니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
  
|Description|지원되는 스토리지 유형|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|데이터 루트 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소 <sup>1</sup>|C:\Program Files\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \| [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성에 대 한 Acl [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리 및 구성의 일부분으로 상속을 해제 합니다.|  
|사용자 데이터베이스 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소 <sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data|사용자 데이터 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.|  
|사용자 데이터베이스 로그 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소 <sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|임시 DB 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소 <sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data|Temp 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.|  
|임시 DB 로그 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소 <sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|백업 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소 <sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Backup|데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 위한 사용자 계정에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
 <sup>1</sup> 공유 디스크가 지원 되지만 권장 되지 않습니다는 독립 실행형 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 장애 조치(failover) 클러스터 인스턴스에 대한 지원되는 스토리지 유형 및 기본 디렉터리를 보여 줍니다.  
  
|Description|지원되는 스토리지 유형|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|데이터 루트 디렉터리|공유 스토리지, SMB 파일 서버|\<드라이브:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> 팁:  **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.|  
|사용자 데이터베이스 디렉터리|공유 스토리지, SMB 파일 서버|\<Drive:>Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data<br /><br /> 팁:  **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|사용자 데이터 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.|  
|사용자 데이터베이스 로그 디렉터리|공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data<br /><br /> 팁:  **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|임시 DB 디렉터리|로컬 디스크, 공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data<br /><br /> 팁:  **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|지정한 디렉터리가 모든 클러스터 노드에 유효한지 확인하십시오. 장애 조치(failover) 중에 장애 조치 대상 노드에서 tempdb 디렉터리를 사용할 수 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스가 온라인이 될 수 없습니다.|  
|임시 DB 로그 디렉터리|로컬 디스크, 공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data<br /><br /> 팁:  **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|지정한 디렉터리가 모든 클러스터 노드에 유효한지 확인하십시오. 장애 조치(failover) 중에 장애 조치 대상 노드에서 tempdb 디렉터리를 사용할 수 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스가 온라인이 될 수 없습니다.|  
|백업 디렉터리|로컬 디스크, 공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Backup<br /><br /> 팁:  **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 SQL Server 서비스를 위한 사용자 계정에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
## <a name="security-considerations"></a>보안 고려 사항  
 설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.  
  
 SMB 파일 서버에는 다음과 같은 권장 사항이 적용됩니다.  
  
-   SMB 파일 서버가 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정은 도메인 계정이어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정은 데이터 디렉터리로 사용되는 SMB 파일 공유 폴더에 대해 FULL CONTROL NTFS 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정에는 SMB 파일 서버에 대한 SeSecurityPrivilege 권한이 부여되어야 합니다. 이 권한을 부여하려면 파일 서버의 로컬 보안 정책 콘솔을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 계정을 **감사 및 보안 로그 관리** 정책에 추가합니다. 이 설정은 **로컬 보안 정책** 콘솔의 **로컬 정책** 에 있는 **사용자 권한 지정** 섹션에서 사용할 수 있습니다.  
  
## <a name="notes"></a>참고  
  
-   기존 설치에 기능을 추가할 경우 이전에 설치한 기능의 위치를 변경할 수 없으며 새 기능의 위치를 지정할 수도 없습니다.  
  
-   기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소도 별도의 디렉터리에 설치해야 합니다.  
  
-   다음과 같은 위치에는 프로그램 파일 및 데이터 파일을 설치할 수 없습니다.  
  
    -   이동식 디스크 드라이브  
  
    -   압축 파일 시스템  
  
    -   시스템 파일이 있는 디렉터리  
  
    -   장애 조치(failover) 클러스터 인스턴스의 매핑된 네트워크 드라이브  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [파일 서버의 공유 및 NTFS 권한](https://go.microsoft.com/fwlink/?LinkID=206571)  
  
  
