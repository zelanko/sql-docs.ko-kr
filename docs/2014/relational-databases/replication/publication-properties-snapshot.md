---
title: 게시 속성, 스냅숏 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.snapshotformat.f1
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d238cd2bce87f65c1d29936457e2b966eee40a5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37214903"
---
# <a name="publication-properties-snapshot"></a>게시 속성, 스냅숏
  **게시 속성** 대화 상자의 **스냅숏** 페이지를 사용하여 스냅숏 형식, 스냅숏 폴더 위치 및 스냅숏 적용 전후 실행할 스크립트를 설정할 수 있습니다. 스냅숏 폴더를 공유로 지정해야 하며 파일을 읽고 폴더에 쓰는 에이전트에 대한 충분한 권한이 있어야 합니다. 폴더의 적절한 보안 유지 방법에 대한 자세한 내용은 [스냅숏 폴더 보안 설정](security/secure-the-snapshot-folder.md)을 참조하세요.  
  
> [!NOTE]  
>  게시 속성을 변경하려면 게시에 대한 새 스냅숏이 필요합니다. 자세한 내용은 [게시 및 아티클 속성 변경](publish/change-publication-and-article-properties.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **스냅숏 형식**  
 스냅숏 형식에 대해 네이티브 모드 또는 문자 모드를 선택합니다.  
  
-   모든 구독자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 아닌 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 인스턴스인 경우 **네이티브 SQL Server - 모든 구독자는 SQL Server를 실행하는 서버여야 합니다** 를 선택합니다. 네이티브 스냅숏 형식을 사용할 때 최상의 성능을 제공합니다.  
  
-   구독자가 **에서 실행되고 있거나** 이외 구독자인 경우 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 문자 - 게시자 또는 구독자가 SQL Server를 실행하지 않는 경우 필요합니다[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택합니다.  
  
 **스냅숏 파일 위치**  
 스냅숏 파일을 저장할 위치를 선택합니다. 파일을 기본 위치에 저장할 수 있으며 기본 위치 대신 대체 위치에 저장할 수도 있습니다. 대체 위치에 저장된 파일을 압축할 수 있습니다.  
  
-   게시자에 대해 기본 스냅숏 폴더를 사용하려면 **기본 폴더에 파일 보관** 을 선택합니다. 스냅숏 폴더 위치는 **배포자 속성** 대화 상자에서 게시자에 대해서만 변경할 수 있으므로 이 대화 상자에서는 읽기 전용입니다. 자세한 내용은 [기본 스냅숏 위치 지정&#40;SQL Server Management Studio&#41;](specify-the-default-snapshot-location-sql-server-management-studio.md)을 참조하세요.  
  
-   기본 위치 대신 대체 위치를 지정하려면 **다음 폴더에 파일 보관** 을 선택합니다. 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하고 위치를 탐색합니다. 대체 스냅숏 위치의 파일을 압축하려면 **이 폴더에 있는 스냅숏 파일 압축** 을 선택합니다. 대체 위치는 다른 서버, 네트워크 드라이브 또는 이동식 미디어(CD-ROM 또는 이동식 디스크 등)가 될 수 있습니다. 자세한 내용은 [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md) 및 [Compressed Snapshots](compressed-snapshots.md)를 참조하세요.  
  
 **추가 스크립트 실행**  
 구독자에 스냅숏 적용 전후에 실행할 스크립트를 지정합니다. **스냅숏 형식** 이 **문자**인 경우에는 스크립트를 지정할 수 없습니다.  
  
 스크립트는 선택 사항이지만 명령을 실행하고 구독자에 관리 변경 내용을 적용하는 편리한 방법을 제공합니다. 스크립트 실행에 대한 자세한 내용은 [스냅숏 적용 전후에 스크립트 실행](execute-scripts-before-and-after-the-snapshot-is-applied.md)을 참조하세요.  
  
-   **스냅숏 적용 전 다음 스크립트 실행** 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하여 스크립트의 위치를 지정합니다.  
  
-   **스냅숏 적용 후 다음 스크립트 실행** 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하여 스크립트의 위치를 지정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Create a Publication](publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)   
 [초기 스냅숏 만들기 및 적용](create-and-apply-the-initial-snapshot.md)   
 [스냅숏으로 구독 초기화](initialize-a-subscription-with-a-snapshot.md)   
 [데이터 및 데이터베이스 개체 게시](publish/publish-data-and-database-objects.md)  
  
  
