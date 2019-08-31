---
title: '1단원: Azure Storage 계정 및 컨테이너 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 69d09b5b058af3404226905bdbe0ef83f33982cf
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176172"
---
# <a name="lesson-1-create-azure-storage-account-and-container"></a>1단원: Azure Storage 계정 및 컨테이너 만들기
  Azure Storage에서 SQL Server 데이터 파일 저장을 시작 하려면 먼저 Azure Storage 계정과 blob 컨테이너 및 공유 액세스 서명을 만들어야 합니다. 1 단원에서는 Azure 관리 포털에 로그인 하 여 저장소 계정, blob 컨테이너 및 공유 액세스 서명을 만드는 과정을 단계별로 안내 합니다.  
  
 기본적으로 스토리지 계정의 소유자만 해당 계정 내에서 BLOB, 테이블 및 큐에 액세스할 수 있습니다. 스토리지 계정 액세스 키를 공유하지 않고 이 새로운 향상된 SQL Server 기능을 사용하여 이러한 리소스에 액세스할 수 있으려면 다음을 수행해야 합니다.  
  
-   컨테이너의 사용 권한을 프라이빗으로 설정합니다.  
  
-   공유 액세스 서명을 만듭니다. 이 서명을 사용하면 리소스를 사용할 수 있는 간격과 클라이언트에 부여할 사용 권한을 지정하여 컨테이너, BLOB, 테이블 또는 큐 리소스에 대한 제한된 액세스를 위임할 수 있습니다.  
  
-   저장된 액세스 정책을 사용하여 컨테이너 또는 해당 BLOB에 대한 공유 액세스 서명을 관리합니다. 저장된 액세스 정책을 통해 공유 액세스 서명을 추가로 제어할 수 있을 뿐만 아니라 간단하게 취소할 수도 있습니다.  
  
 자세한 내용은 [Azure Storage 리소스에 대 한 액세스 관리](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx)를 참조 하세요.  
  
## <a name="create-storage-account"></a>스토리지 계정 만들기  
 Azure 관리 포털에서 저장소 계정을 만들려면 다음 단계를 수행 합니다.  
  
1.  계정을 사용 하 여 [Azure 관리 포털](https://manage.windowsazure.com) 에 로그인 합니다. Azure 계정이 없는 경우 [azure 무료 평가판](http://www.windowsazure.com/pricing/free-trial/)을 방문 하세요.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  단계별 지침을 사용하여 [스토리지 계정을 만듭니다](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/). Azure의 SQL Server 데이터 파일 기능에 사용할 저장소 계정을 만드는 경우 지역에서 복제를 선택 취소 하거나 사용 하지 않도록 설정 해야 합니다. 이는 지리적 복제에 참여하는 여러 BLOB에 대해 쓰기 순서가 보장되지 않기 때문입니다. 스토리지 계정이 지리적으로 복제되고 복구가 필요한 경우 손상이 발생합니다.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>BLOB 컨테이너 만들기  
 Azure에서 컨테이너는 blob 집합의 그룹화를 제공 합니다. 모든 blob는 컨테이너에 있어야 합니다. 스토리지 계정은 개수에 제한 없이 컨테이너를 포함할 수 있지만 적어도 하나는 포함해야 합니다. 컨테이너에는 개수에 제한 없이 blob를 저장할 수 있습니다. 저장소 크기 제한에 대 한 최신 정보는 [.net에서 Azure Blob Storage 서비스를 사용 하는 방법](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)을 참조 하세요.  
  
 Azure에서 컨테이너를 만들려면 다음 단계를 수행 합니다.  
  
1.  [Azure 관리 포털](https://manage.windowsazure.com)에 로그인 합니다.  
  
2.  스토리지 계정을 선택하고 **컨테이너** 탭을 클릭한 다음 화면 맨 아래에서 **컨테이너 추가** 를 클릭하면 새 대화 상자가 열립니다.  
  
3.  컨테이너 이름을 입력합니다.  
  
4.  **액세스 형식** 에서 **개인**을 선택합니다. 액세스 권한을 개인으로 설정 하는 경우 Azure 계정 소유자만 컨테이너 및 blob 데이터를 읽을 수 있습니다.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  프로그래밍 방식으로 컨테이너를 만들려면 REST API를 사용할 수도 있습니다. 자세한 내용은 [컨테이너 만들기](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx) 및 [Azure Storage 서비스 REST API 참조](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx)를 참조 하세요.  
  
 **다음 단원:**  
  
 [2단원. 컨테이너에서 정책을 만들고 공유 액세스 서명 &#40;SAS&#41; 키 생성](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
  
