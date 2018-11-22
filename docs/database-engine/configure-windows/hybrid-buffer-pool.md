---
title: 하이브리드 버퍼 풀 | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.openlocfilehash: a8098c38b72ba44ab973fe5564b93740252bafc6
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560310"
---
# <a name="hybrid-buffer-pool"></a>하이브리드 버퍼 풀
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2019 CTP 2.1에서는 PMEM(영구 메모리) 디바이스에 저장된 데이터베이스 파일의 데이터 페이지에 직접 액세스할 수 있게 하는 새 기능이 SQL Server 데이터베이스 엔진에 도입되었습니다. 

영구 메모리가 없는 기존 시스템에서는 SQL Server가 버퍼 풀에 데이터 페이지를 캐시합니다. 하이브리드 버퍼 풀을 사용하면 SQL Server가 페이지를 버퍼 풀의 DRAM 부분에 복사하는 대신에, PMEM 디바이스에 상주하는 데이터베이스 파일에서 직접 페이지를 참조합니다. 하이브리드 버퍼 풀에 대한 PMEM의 데이터 파일 액세스는 메모리 매핑된 I/O를 통해 수행되며 enlightenment라고도 합니다.

클린 페이지만 PMEM 디바이스에서 직접 참조할 수 있습니다. 더티 페이지가 되면 DRAM에 보관되며 결과적으로 PMEM 디바이스에 다시 작성됩니다.

이 기능은 Windows와 Linux 모두에서 사용할 수 있습니다.

## <a name="enable-hybrid-buffer-pool"></a>하이브리드 버퍼 풀 사용

CTP 2.1에서 하이브리드 버퍼 풀을 사용하려면 시작 추적 플래그 809를 설정해야 합니다.

## <a name="best-practices-for-hybrid-buffer-pool"></a>하이브리드 버퍼 풀 모범 사례

* Windows에서 PMEM 디바이스를 포맷할 때 NTFS에 가능한 가장 큰 할당 단위를 사용하고(Windows Server 2019에서 2MB) 디바이스에서 DAX(DirectAccess)가 사용하도록 설정되었는지 확인합니다.
  