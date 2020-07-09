---
title: 가상 디바이스 인터페이스 참조
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 SQL Server 백업에 대한 가상 디바이스 인터페이스 참조를 대략적으로 설명합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0bacc2d49424aa9f8266a993a58546a80385aced
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893086"
---
# <a name="virtual-device-interface-vdi-reference"></a>VDI(가상 디바이스 인터페이스) 참조

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

이 섹션에는 타사 백업 소프트웨어 공급업체용으로 작성된 SQL Server 애플리케이션 프로그래밍 인터페이스의 사양이 나와 있습니다.

## <a name="overview"></a>개요

VDI(가상 디바이스 인터페이스)는 가장 빠른 복원 시간뿐만 아니라 트랜잭션 워크로드에 대한 성능 저하를 최소화하면서 최고 수준의 온라인 백업 처리량을 제공합니다. 이를 통해 타사 공급업체는 SQL Server 네이티브 백업/복원과 동일한 성능 특성을 얻을 수 있으며 전체 백업/복원 기능을 사용할 수 있습니다. VDI는 SQL Server 7.0에 도입되었으며 이후 버전에서도 지원되고 개선되었습니다.

VDI는 다음과 같은 두 가지 기본 유형의 백업 기술을 지원합니다.

- 백업 세트의 전체 내용을 읽고 백업 미디어로 전송하는 기존 온라인 백업

- 기본 분할 미러 또는 기록 중 복사 기술을 사용하는 스냅샷 백업

VDI를 통해 수행되는 기존의 온라인 백업은 SQL Server의 백업 및 복원 기능을 모두 활용할 수 있습니다. 스냅샷 백업은 전체 데이터베이스 및 파일/파일 그룹 백업으로만 제한됩니다. 그러나 스냅샷 백업은 기존 데이터베이스 차등, 파일 차등 및 트랜잭션 로그 백업과 함께 롤포워드할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 섹션의 VDI 참조 설명서를 검토합니다.

전체 사양과 지원되는 원본 파일을 다운로드합니다.

[SQL Server 2005 VDI(가상 백업 디바이스 인터페이스) 사양](https://www.microsoft.com/download/details.aspx?id=17282)