---
title: SQL 복제에 대한 스냅숏 초기화 옵션 수정 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68e61f26cc33d505ec183e3d863cfa3a6f407275
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586427"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>SQL 복제에 대한 스냅숏 초기화 옵션 수정 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[스냅숏으로 구독을 초기화](initialize-a-subscription-with-a-snapshot.md)할 때 지정할 수 있는 여러 옵션이 있습니다.

## <a name="specify-snapshot-format-sql-server-management-studio"></a>스냅숏 형식 지정(SQL Server Management Studio)
  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에서 스냅숏 형식을 지정합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-specify-snapshot-format"></a>스냅숏 형식을 지정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에서 **네이티브 SQL Server - 모든 구독자는 SQL Server를 실행하는 서버여야 합니다** 또는 **문자 - 게시자 또는 구독자가 SQL Server를 실행하지 않는 경우 필요합니다**를 선택합니다.  
  
    > [!NOTE]  
    >  이 게시가 SQL Server Compact 데이터베이스 또는 SQL Server 이외의 데이터베이스에 대한 구독을 지원해야 하는 경우가 아니면 네이티브 형식을 선택하는 것이 좋습니다.  
  
2.  **확인**을 선택합니다.   

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="snapshot-folder-locations"></a>스냅숏 폴더 위치

### <a name="default-snapshot-location"></a>기본 스냅숏 위치
배포 구성 마법사의 **스냅숏 폴더** 페이지에서 기본 스냅숏 위치를 지정합니다. 이 마법사 사용에 대한 자세한 내용은 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)을 참조하세요. 배포자로 구성되어 있지 않은 서버에서 게시를 만드는 경우 새 게시 마법사의 **스냅숏 폴더** 페이지에서 기본 스냅숏 위치를 지정합니다. 이 마법사를 사용하는 방법에 대한 자세한 내용은 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
 **배포자 속성 - \<Distributor>** 대화 상자의 **게시자** 페이지에서 기본 스냅숏 위치를 수정합니다. 자세한 내용은 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요. **게시 속성 - \<게시>** 대화 상자에서 각 게시에 대한 스냅숏 폴더를 설정합니다. 자세한 내용은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-modify-the-default-snapshot-location"></a>기본 스냅숏 위치를 수정하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **게시자** 페이지에서 기본 스냅샷 위치를 변경하려는 게시자의 속성 단추( **?** )를 클릭합니다.    
2.  **게시자 속성 - \<Publisher>** 대화 상자에서 **기본 스냅숏 폴더** 속성에 대한 값을 입력합니다.  
  
    > [!NOTE]  
    >  스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.    
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
 

### <a name="alternate-snapshot-locations"></a>대체 스냅숏 위치
대체 스냅숏 위치를 사용하면 기본 위치가 아닌 위치(일반적으로 배포자에 위치)에 스냅숏 파일을 저장할 수 있습니다. 대체 위치는 다른 서버, 다른 네트워크 드라이브 또는 이동식 미디어(CD-ROM, 이동식 디스크)가 될 수 있습니다.  
  
대체 스냅숏 위치는 게시의 속성으로 저장됩니다. 대체 스냅숏 위치가 게시 속성이기 때문에 배포 에이전트 및 병합 에이전트에서는 동화 프로세스의 일부인  올바른 스냅숏을 찾을 수 있습니다.  
  
대체 스냅숏 폴더 위치를 지정하거나 스냅숏 파일을 압축하려면 초기 스냅숏을 즉시 만들지 말고 게시를 만들어 스냅숏 위치에 대한 게시 속성을 설정한 다음 해당 게시에 대해 스냅숏 에이전트를 실행합니다. 초기 스냅숏을 만든 다음 대체 위치를 변경할 경우 게시에 대해 생성된 스냅숏의 위치는 새 대체 위치로 다시 지정할 수 없습니다. 이 경우 게시 설정에 따라 병합 에이전트나 배포 에이전트가 새 대체 위치에서 스냅숏 파일을 찾지 못할 수 있습니다.  
  
> [!NOTE]  
>  대체 위치를 기본 스냅숏 폴더 위치와 동일하게 지정하지 마세요. 대체 위치는 **게시 속성** 대화 상자나 [sp_changepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 사용하여 지정할 수 있습니다.  
  
> [!CAUTION]  
>  WebSync 및 대체 스냅숏 폴더 위치를 동시에 사용하지 마십시오.  
  
#### <a name="use-sql-server-management-studio"></a>SQL Server Management Studio 사용
1.  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에서 다음을 수행합니다.  
  
    1.  **다음 폴더에 파일 보관**을 선택한 다음 **찾아보기** 를 클릭하여 디렉터리로 이동하거나 스냅숏 파일을 저장할 디렉터리 경로를 입력합니다.  
  
        > [!NOTE]  
        >  스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  
    2.  두 위치 모두에 스냅숏 파일을 쓸 필요가 없으면 **기본 폴더에 파일 보관** 의 선택을 취소합니다.  
  
     스냅숏 파일을 압축하려면 **이 폴더에 있는 스냅숏 파일 압축**을 선택합니다. 압축은 일반적으로 느린 대역폭 연결에 사용되며 CD-ROM 등의 이동식 미디어와 같은 대체 스냅숏 위치로 사용됩니다.  
  
2.  **확인**을 선택합니다.  
  
#### <a name="use-transact-sql"></a>Transact-SQL 사용 

[스냅숏 속성 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md) 시 **snapshot_in_defaultfolder**의 값을 false로 지정합니다. 

## <a name="compressed-snapshots"></a>압축 스냅숏
  스냅숏을 느린 네트워크를 통해 전송하거나 이동식 미디어에 저장할 때 압축하지 않은 스냅숏이 너무 커서 해당 미디어에 모두 저장할 수 없는 경우 스냅숏 파일을 압축하는 것이 좋습니다. 위와 같은 상황에서는 스냅숏 파일을 압축하는 것이 유용하지만 압축으로 인해 스냅숏 생성과 적용에 더 많은 시간이 걸립니다.  
  
 압축 스냅숏 파일은 2GB 이하의 파일만 압축할 수 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 파일 형식으로 작성됩니다. 스냅숏 파일이 2GB보다 크면 압축할 수 없습니다. 파일을 압축하려면 해당 파일을 대체 스냅숏 폴더에 기록해야 합니다. 기본 스냅숏 폴더에 기록한 파일은 압축할 수 없습니다. 
  
 압축 파일은 배포 에이전트 또는 병합 에이전트가 실행되는 위치에 풀립니다. 압축 파일이 구독자에 풀리도록 압축 스냅숏에는 일반적으로 끌어오기 구독이 사용됩니다. 구독자가 압축 파일을 받으면 이 파일은 일단 임시 위치에 기록됩니다. 압축 파일을 구독자로 복사하고 나면 CAB 유틸리티에 의해 한 번에 한 파일씩 순서대로 파일의 압축이 해제됩니다. 구독자에 필요한 공간은 압축 스냅숏 파일에 가장 큰 압축 해제 파일의 크기를 더한 값입니다.  
  
> [!NOTE]  
>  스냅숏을 압축하면 네트워크에서의 스냅숏 파일 전송 성능이 향상되는 경우도 있습니다. 그러나 스냅숏 에이전트에서 스냅숏 파일을 생성하는 경우와 배포 에이전트 또는 병합 에이전트에서 스냅숏 파일을 적용하는 경우에 스냅숏 파일을 압축하려면 추가 처리 작업이 필요합니다. 이 경우 스냅숏 생성 속도가 느려지거나 스냅숏 적용 시간이 늘어날 수 있습니다. 또한 네트워크 오류가 발생하면 압축 스냅숏은 재개할 수 없으므로 불안정한 네트워크에서는 압축 스냅숏이 적합하지 않습니다. 네트워크에서 압축 스냅숏을 사용하는 경우 이러한 장단점을 신중하게 고려하여 균형을 맞추는 것이 좋습니다.  
  
### <a name="use-sql-server-management-studio"></a>SQL Server Management Studio 사용
1.  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에서 다음을 수행합니다.  
  
    1.  **다음 폴더에 파일 보관**을 선택한 다음 **찾아보기** 를 클릭하여 디렉터리로 이동하거나 스냅숏 파일을 저장할 디렉터리 경로를 입력합니다.  
  
        > [!NOTE]  
        >  스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안 설정](security/secure-the-snapshot-folder.md)을 참조하세요.  
  
    2.  두 위치 모두에 스냅숏 파일을 쓸 필요가 없으면 **기본 폴더에 파일 보관** 의 선택을 취소합니다.  
  
        > [!NOTE]  
        >  이 확인란을 선택하면 기본 폴더에 저장된 파일은 압축되지 않습니다. 압축 파일은 이전 단계에서 지정한 대체 위치에만 저장할 수 있습니다.  
  
2.  **이 폴더에 있는 스냅숏 파일 압축**을 선택합니다.    
3.  **확인**을 선택합니다.   

### <a name="use-transact-sql"></a>Transact-SQL 사용

[스냅숏 속성 구성](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md) 시 **compress_snapshot** 값을 **True**로 지정합니다. 

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>스냅숏 적용 전후에 스크립트 실행
스냅숏 적용 전후에 구독자에서 스크립트가 실행되도록 지정할 수 있습니다. 각 구독자에서 로그인과 스키마(개체 소유자)를 만드는 작업 등 다양한 작업에 스크립트를 사용할 수 있습니다.  
  
 사용자가 각 스크립트에 대한 파일 위치를 지정하면 스냅숏 에이전트는 스냅숏 처리가 발생할 때마다 해당 스크립트 파일을 현재 스냅숏 폴더로 복사합니다. 배포 에이전트 또는 병합 에이전트는 스냅숏을 적용할 때 복제된 모든 개체 스크립트보다 먼저 프리 스냅숏 스크립트를 실행합니다. 배포 에이전트 또는 병합 에이전트는 복제된 다른 개체 스크립트 및 데이터가 모두 적용된 후에 포스트 스냅숏 스크립트를 실행합니다. 스냅숏 애플리케이션이 완료되고 스크립트 파일이 성공적으로 실행되면 스크립트 파일은 구독자의 작업 디렉터리에서 제거됩니다.  
  
 스크립트는 **sqlcmd** 유틸리티를 시작하여 실행합니다. 스크립트를 배포하기 전에 **sqlcmd** 로 스크립트를 실행하여 예상된 대로 실행되는지 확인합니다. 스냅숏 적용 전후에 실행되는 스크립트의 내용은 반복 가능해야 합니다. 예를 들어 스크립트로 테이블을 만들려면 먼저 테이블이 존재하는지 확인하고 테이블이 존재하면 적절한 조치를 취해야 합니다. 스크립트가 이미 적용된 구독을 다시 초기화할 필요가 있다면 다시 초기화하는 중에 새 스냅숏이 적용될 때 스크립트도 다시 적용될 것이기 때문에 스크립트는 반복 가능해야 합니다.  
  
 스냅숏 파일을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 파일 형식으로 압축하는 중이면 스크립트도 압축되어 CAB 파일 내에 위치합니다. 압축 스냅숏 파일을 구독자로 전송하고 구독자의 작업 디렉터리로 압축을 풀면 프리 스냅숏 스크립트로 표시된 모든 스크립트가 실행됩니다. 마찬가지로 모든 포스트 스냅숏 스크립트도 압축이 풀리고 스냅숏 적용의 마지막 단계로 구독자에서 실행됩니다.  

### <a name="execute-a-script"></a>스크립트 실행 

1.  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에서 다음을 수행합니다.    
    -   스냅숏이 적용되기 전에 실행할 스크립트를 지정하려면 **찾아보기** 를 클릭하여 스크립트로 이동하거나 **스냅숏 적용 전 다음 스크립트 실행** 입력란에 스크립트의 경로를 입력합니다.  
  
        > [!NOTE]  
        >  배포 에이전트 또는 병합 에이전트에는 지정한 디렉터리에 대한 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\scripts\myscript.sql과 같이 UNC(Universal Naming Convention) 경로로 지정해야 합니다.  
  
    -   스냅숏이 적용된 후에 실행할 스크립트를 지정하려면 **찾아보기** 를 클릭하여 스크립트로 이동하거나 **스냅숏 적용 후 다음 스크립트 실행** 입력란에 스크립트의 UNC 경로를 입력합니다.   
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  


## <a name="see-also"></a>참고 항목  
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [FTP를 통해 스냅숏 전송](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)   
 [스냅숏 속성 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)     
  
  
