---
title: 연결 풀링
description: ADO.NET에서 데이터 원본에 대한 연결을 여는 비용을 최소화하기 위해 사용하는 최적화 기술인 연결 풀링에 대해 알아봅니다.
ms.date: 11/13/2020
ms.assetid: 955c057f-aea8-4ba8-aa6d-e3dfa18ba8d5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 41b139d2f22a9cb3137879d96224b02eafc24bab
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761501"
---
# <a name="connection-pooling"></a>연결 풀링

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

데이터 소스에 연결하는 작업은 시간이 많이 걸릴 수 있습니다. 연결을 여는 비용을 최소화하기 위해 ADO.NET에서는 *연결 풀링* 이라는 최적화 기법을 사용합니다. 이 기법을 사용하면 연결을 반복적으로 열고 닫는 데 드는 비용을 최소화할 수 있습니다.

## <a name="in-this-section"></a>섹션 내용  

[SQL Server 연결 풀링(ADO.NET)](sql-server-connection-pooling.md)  
연결 풀링에 대해 간략하게 설명하고 SQL Server에서 연결 풀링이 작동하는 방식을 설명합니다.

## <a name="see-also"></a>참고 항목

- [ADO.NET에서 데이터 검색 및 수정](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
