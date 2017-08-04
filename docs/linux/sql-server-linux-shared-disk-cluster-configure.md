---
title: "Linux에서 SQL Server에 대 한 공유 디스크 클러스터를 구성 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92b4cb2500d4fd8a1643488593c40e97b1ff6454
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---

# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>Linux에서 SQL Server에 대 한 공유 디스크 클러스터

와 다른 한 노드에서 장애 조치에는 SQL Server 인스턴스를 허용 하는 Linux 공유 저장소 고가용성 클러스터를 구성할 수 있습니다. 일반적인 클러스터에 두 개 이상의 서버 공유 저장소에 연결 됩니다. 서버는 클러스터 노드입니다. 장애 조치 클러스터 SQL Server를 두 개 이상의 노드 간 장애 조치를 허용 하 여 복구 시간을 개선 하기 위해 인스턴스 수준의 보호를 제공 합니다. 구성 단계는 Linux 배포판 및 솔루션 클러스터링에 따라 다릅니다. 다음 표에서 유효성이 검사 된 클러스터 솔루션에 대 한 특정 단계를 보여 줍니다.  

|배포 |항목 
|----- |-----
|**Red Hat Enterprise Linux HA 추가 기능 사용** |[구성](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[작동](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server HA 추가 기능 사용** |[구성](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>다음 단계


