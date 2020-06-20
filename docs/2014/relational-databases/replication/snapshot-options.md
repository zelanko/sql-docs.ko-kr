---
title: SQL 복제에 대한 스냅샷 초기화 옵션 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 946d9035730512a626e710b1140a1ba01290908a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055639"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>SQL 복제에 대한 스냅샷 초기화 옵션 수정

이 문서에서는 [스냅숏으로 구독을 초기화할](initialize-a-subscription-with-a-snapshot.md)때 다양 한 옵션을 수정 하는 방법을 설명 합니다.

## <a name="snapshot-format"></a>스냅숏 형식
  **게시 속성- \<Publication> ** 대화 상자의 **스냅숏** 페이지에서 스냅숏 형식을 지정 합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)을 참조하세요.  

1.  **게시 속성- \<Publication> ** 대화 상자의 **스냅숏** 페이지에서 네이티브 SQL Server를 선택 **합니다. 모든 구독자는 SQL Server를 실행** 하는 서버 여야 합니다. 또는 **게시자 또는 구독자가 SQL Server를 실행 하 고 있지 않은 경우 필수**입니다. 

    > [!NOTE]  
    >  이 게시가 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 데이터베이스 또는[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외의 데이터베이스에 대한 구독을 지원해야 하는 경우가 아니면 네이티브 형식을 선택하는 것이 좋습니다.    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="snapshot-folder-locations"></a>스냅숏 폴더 위치

### <a name="default-snapshot-location"></a>기본 스냅샷 위치
기본 스냅숏 위치 (SQL Server Management Studio) 지정 배포 구성 마법사의 **스냅숏 폴더** 페이지에서 기본 스냅숏 위치를 지정 합니다. 이 마법사 사용에 대한 자세한 내용은 [게시 및 배포 구성](configure-publishing-and-distribution.md)을 참조하세요. 배포자로 구성되어 있지 않은 서버에서 게시를 만드는 경우 새 게시 마법사의 **스냅샷 폴더** 페이지에서 기본 스냅샷 위치를 지정합니다. 이 마법사를 사용하는 방법에 대한 자세한 내용은 [게시 만들기](publish/create-a-publication.md)를 참조하세요.  
  
 **배포자 속성- \<Distributor> ** 대화 상자의 **게시자** 페이지에서 기본 스냅숏 위치를 수정 합니다. 자세한 내용은 [배포자 및 게시자 속성 보기 및 수정](view-and-modify-distributor-and-publisher-properties.md)을 참조하세요. **게시 속성- \<Publication> ** 대화 상자에서 각 게시에 대 한 스냅숏 폴더를 설정 합니다. 자세한 내용은 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="modify-the-default-snapshot-location"></a>기본 스냅샷 위치 수정  
  
1.  **배포자 속성- \<Distributor> ** 대화 상자의 **게시자** 페이지에서 기본 스냅숏 위치를 변경할 게시자의 속성 단추 (**...**)를 클릭 합니다.    
2.  **게시자 속성- \<Publisher> ** 대화 상자에서 **기본 스냅숏 폴더** 속성에 대 한 값을 입력 합니다.

    > [!NOTE]  
    >  스냅샷 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안](security/secure-the-snapshot-folder.md)설정을 참조 하세요.    
1.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

### <a name="alternate-snapshot-location"></a>대체 스냅숏 위치
  **게시 속성- \<Publication> ** 대화 상자의 **스냅숏** 페이지에서 대체 스냅숏 위치를 지정 합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)을 참조하세요. 

  
#### <a name="specify-an-alternate-snapshot-location"></a>대체 스냅숏 위치 지정  
  
1.  **게시 속성- \<Publication> ** 대화 상자의 **스냅숏** 페이지에서 다음을 수행 합니다.    
    1.  **다음 폴더에 파일 보관**을 선택한 다음 **찾아보기** 를 클릭하여 디렉터리로 이동하거나 스냅샷 파일을 저장할 디렉터리 경로를 입력합니다.    

        > [!NOTE]  
        >  스냅샷 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안](security/secure-the-snapshot-folder.md)설정을 참조 하세요.    
    a.  두 위치 모두에 스냅샷 파일을 쓸 필요가 없으면 **기본 폴더에 파일 보관** 의 선택을 취소합니다.    
     스냅샷 파일을 압축하려면 **이 폴더에 있는 스냅샷 파일 압축**을 선택합니다. 압축은 일반적으로 느린 대역폭 연결에 사용되며 CD-ROM 등의 이동식 미디어와 같은 대체 스냅샷 위치로 사용됩니다.    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]   


## <a name="compress-snapshot-files"></a>스냅숏 파일 압축
**게시 속성- \<Publication> ** 대화 상자의 **스냅숏** 페이지에서 파일을 압축 하도록 지정 합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
1.  **게시 속성- \<Publication> ** 대화 상자의 **스냅숏** 페이지에서 다음을 수행 합니다.  
  
    1.  **다음 폴더에 파일 보관**을 선택한 다음 **찾아보기** 를 클릭하여 디렉터리로 이동하거나 스냅샷 파일을 저장할 디렉터리 경로를 입력합니다.    
        > [!NOTE]  
        >  스냅샷 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅샷 폴더 보안 설정](security/secure-the-snapshot-folder.md)을 참조하세요.  
  
    2.  두 위치 모두에 스냅샷 파일을 쓸 필요가 없으면 **기본 폴더에 파일 보관** 의 선택을 취소합니다.    
        > [!NOTE]  
        >  이 확인란을 선택하면 기본 폴더에 저장된 파일은 압축되지 않습니다. 압축 파일은 이전 단계에서 지정한 대체 위치에만 저장할 수 있습니다.    
2.  **이 폴더에 있는 스냅샷 파일 압축**을 선택합니다.    
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>스냅샷 적용 전후에 스크립트 실행

 스냅샷 적용 전후에 구독자에서 스크립트가 실행되도록 지정할 수 있습니다. 각 구독자에서 로그인과 스키마(개체 소유자)를 만드는 작업 등 다양한 작업에 스크립트를 사용할 수 있습니다.  
  
 사용자가 각 스크립트에 대한 파일 위치를 지정하면 스냅샷 에이전트는 스냅샷 처리가 발생할 때마다 해당 스크립트 파일을 현재 스냅샷 폴더로 복사합니다. 배포 에이전트 또는 병합 에이전트는 스냅샷을 적용할 때 복제된 모든 개체 스크립트보다 먼저 프리 스냅샷 스크립트를 실행합니다. 배포 에이전트 또는 병합 에이전트는 복제된 다른 개체 스크립트 및 데이터가 모두 적용된 후에 포스트 스냅샷 스크립트를 실행합니다. 스냅샷 애플리케이션이 완료되고 스크립트 파일이 성공적으로 실행되면 스크립트 파일은 구독자의 작업 디렉터리에서 제거됩니다.  
  
 스크립트는 **sqlcmd** 유틸리티를 시작하여 실행합니다. 스크립트를 배포하기 전에 **sqlcmd** 로 스크립트를 실행하여 예상된 대로 실행되는지 확인합니다. 스냅샷 적용 전후에 실행되는 스크립트의 내용은 반복 가능해야 합니다. 예를 들어 스크립트로 테이블을 만들려면 먼저 테이블이 존재하는지 확인하고 테이블이 존재하면 적절한 조치를 취해야 합니다. 스크립트가 이미 적용된 구독을 다시 초기화할 필요가 있다면 다시 초기화하는 중에 새 스냅샷이 적용될 때 스크립트도 다시 적용될 것이기 때문에 스크립트는 반복 가능해야 합니다.  
  
 스냅샷 파일을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 파일 형식으로 압축하는 중이면 스크립트도 압축되어 CAB 파일 내에 위치합니다. 압축 스냅샷 파일을 구독자로 전송하고 구독자의 작업 디렉터리로 압축을 풀면 프리 스냅샷 스크립트로 표시된 모든 스크립트가 실행됩니다. 마찬가지로 모든 포스트 스냅샷 스크립트도 압축이 풀리고 스냅샷 적용의 마지막 단계로 구독자에서 실행됩니다.  

### <a name="execute-a-script-before-or-after-a-snapshot-is-applied"></a>스냅숏 적용 전후에 스크립트 실행  
 **게시 속성- \<Publication> ** 대화 상자의 **스냅숏** 페이지에서 스냅숏 적용 전후에 실행할 선택적 스크립트를 지정 합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)을 참조하세요.  


1.  **게시 속성- \<Publication> ** 대화 상자의 **스냅숏** 페이지에서 다음을 수행 합니다.    
    -   스냅샷이 적용되기 전에 실행할 스크립트를 지정하려면 **찾아보기** 를 클릭하여 스크립트로 이동하거나 **스냅샷 적용 전 다음 스크립트 실행** 입력란에 스크립트의 경로를 입력합니다. 
   
        > [!NOTE]  
        >  배포 에이전트 또는 병합 에이전트에는 지정한 디렉터리에 대한 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\scripts\myscript.sql과 같이 UNC(Universal Naming Convention) 경로로 지정해야 합니다.    
    -   스냅샷이 적용된 후에 실행할 스크립트를 지정하려면 **찾아보기** 를 클릭하여 스크립트로 이동하거나 **스냅샷 적용 후 다음 스크립트 실행** 입력란에 스크립트의 UNC 경로를 입력합니다.    
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
  
