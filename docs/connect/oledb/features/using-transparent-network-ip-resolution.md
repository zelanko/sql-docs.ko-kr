---
description: 투명 네트워크 IP 확인 사용
title: 투명 네트워크 IP 확인 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: chris-rossi
ms.author: v-chross
ms.openlocfilehash: adaad0f80d6304c855af22f134d24f0d3f23d301
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88415019"
---
# <a name="using-transparent-network-ip-resolution"></a>투명 네트워크 IP 확인 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>목적
TNIR(투명 네트워크 IP 확인)은 기존 MultiSubnetFailover 기능의 수정 버전입니다. TNIR은 호스트 이름의 첫 번째 확인된 IP가 응답하지 않고 호스트 이름과 연결된 여러 IP가 있는 경우 드라이버의 연결 시퀀스에 영향을 미칩니다. TNIR은 MultiSubnetFailover와 상호 작용하여 다음과 같은 세 가지 연결 시퀀스를 제공합니다.<br />
* 0: 하나의 IP가 시도된 후 모든 IP가 병렬로 실행됨
* 1: 모든 IP가 병렬로 시도됨
* 2: 모든 IP가 차례대로 하나씩 시도됨

|TransparentNetworkIPResolution|MultiSubnetFailover|동작|
|--------|--------|--------|
|True|True|1|
|참|거짓|0|
|False|True|1|
|False|False|2|

## <a name="setting-transparent-network-ip-resolution"></a>투명 네트워크 IP 확인 설정
TransparentNetworkIPResolution은 기본적으로 사용하도록 설정됩니다. MultiSubnetFailover은 기본적으로 사용하지 않도록 설정됩니다. 다음 페이지에서 이러한 속성 설정에 대한 자세한 정보를 제공합니다. 
- [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](..\applications\using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [초기화 및 권한 부여 속성](..\ole-db-data-source-objects\initialization-and-authorization-properties.md)

## <a name="see-also"></a>참고 항목 
[SQL Server용 OLE DB 드라이버의 고가용성, 재해 복구 지원](./oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)
