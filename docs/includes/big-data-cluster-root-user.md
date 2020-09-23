---
author: MikeRayMSFT
ms.prod: sql
ms.technology: big-data-cluster
ms.topic: include
ms.date: 06/22/2020
ms.author: mikeray
ms.openlocfilehash: b72f8044638adbf75049392fae32447a8a749a6d
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85215152"
---
SQL Server 2019 CU5부터 기본 인증을 사용하여 새 클러스터를 배포하는 경우 게이트웨이를 비롯한 모든 엔드포인트는 `AZDATA_USERNAME` 및 `AZDATA_PASSWORD`를 사용합니다. CU5로 업그레이드된 클러스터의 엔드포인트는 게이트웨이 엔드포인트에 연결하기 위해 사용자 이름으로 `root`를 계속 사용합니다. Active Directory 인증을 사용하는 배포에는 이 변경 내용이 적용되지 않습니다. 릴리스 정보에서 [게이트웨이 엔드포인트를 통해 서비스에 액세스하기 위한 자격 증명](../big-data-cluster/release-notes-big-data-cluster.md#credentials-for-accessing-services-through-gateway-endpoint)을 참조하세요.