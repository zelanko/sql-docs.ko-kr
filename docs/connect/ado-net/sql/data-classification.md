---
title: SqlClient의 데이터 검색 및 분류
description: SQL Server 데이터베이스에서 데이터 분류를 지원하는지 확인하는 방법 및 SqlDataReader 개체를 통해 데이터 분류 정보에 액세스하는 방법을 설명합니다.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 6d82bfd3c49576a35b24f5a04cdc2c03dceeb766
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081502"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>SqlClient의 데이터 검색 및 분류

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[데이터 검색 및 분류](../../../relational-databases/security/sql-data-discovery-and-classification.md)는 데이터베이스에서 중요한 데이터를 검색, 분류, 레이블 지정하기 위한 고급 서비스의 집합입니다. SqlClient는 기본 원본이 기능을 지원하는 경우 읽기 전용 데이터 검색 및 분류 정보를 노출하는 API를 제공합니다. 이 정보는 SqlDataReader를 통해 액세스합니다.

이 샘플 애플리케이션은 SqlDataReader의 데이터 분류 속성에 액세스하는 방법을 보여 줍니다.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**참고 항목**  

 [SQL Server 기능 및 ADO.NET](sql-server-features-adonet.md)