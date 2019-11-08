---
ms.openlocfilehash: 497a564a10a3d35b33f47222fce8f89fe36bd15e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73530943"
---
서버(인스턴스 수준) 설정을 구성하거나 가용성 그룹에 데이터베이스를 수동으로 추가하는 등의 특정 작업을 수행하려면 SQL Server 인스턴스에 연결해야 합니다. 가용성 그룹에 속한 데이터베이스에서 `sp_configure`, `RESTORE DATABASE` 또는 DDL 명령과 같은 작업을 수행하려면 SQL Server 인스턴스에 연결해야 합니다. 기본적으로 빅 데이터 클러스터에는 인스턴스에 연결할 수 있는 엔드포인트가 포함되어 있지 않습니다. 이 엔드포인트는 수동으로 노출해야 합니다.

자세한 내용은 [주 복제본의 데이터베이스에 연결](../big-data-cluster/deployment-high-availability.md#instance-connect)을 참조하세요.