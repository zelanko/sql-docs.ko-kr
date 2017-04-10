---
title: "네트워크 속성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "LingerTimeout 속성"
  - "EnableNagleAlgorithm 속성"
  - "MinPendingAcceptExCount 속성"
  - "MaxPendingSendCount 속성"
  - "EnableBinaryXML 속성"
  - "MinPendingReceiveCount 속성"
  - "MaxCompletedReceiveCount 속성"
  - "DisableNonblockingMode 속성"
  - "RequestSizeThreshold 속성"
  - "CompressionLevel 속성"
  - "ReceiveBufferSize 속성"
  - "EnableCompression 속성"
  - "ServerSendTimeout 속성"
  - "IPV4Support 속성"
  - "MaxPendingReceiveCount 속성"
  - "MaxPendingAcceptExCount 속성"
  - "IPV6Support 속성"
  - "MaxAllowedRequestSize 속성"
  - "ServerReceiveTimeout 속성"
  - "EnableLingerOnClose 속성"
  - "InitialConnectTimeout 속성"
  - "SendBufferSize 속성"
  - "ScatterReceiveMultiplier 속성"
  - "네트워크 속성 [Analysis Services]"
ms.assetid: ef4251e2-abe5-4c5b-9868-7549782d0244
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 15
---
# 네트워크 속성
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 다음 표에 나열된 서버 속성을 사용할 수 있습니다. 추가 서버 속성 및 해당 속성 설정 방법에 대한 자세한 내용은 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)을 참조하세요.  
  
 **적용 대상:** 다차원 및 테이블 형식 서버 모드  
  
## 일반  
 **ListenOnlyOnLocalConnections**  
 로컬 연결(예: localhost)만 수신하는지 여부를 식별하는 부울 속성입니다.  
  
## 수신기  
 **IPV4Support**  
 IPv4 프로토콜에 대한 지원을 정의하는 부호 있는 32비트 정수 속성입니다. 이 속성은 다음 표에 나열된 값 중 하나를 가집니다.  
  
|Value|설명|  
|-----------|-----------------|  
|*0*|IPv4가 해제되어 클라이언트가 연결할 수 없습니다.|  
|*1.*|(기본값) IPv4가 필요하고 IPv4를 수신할 수 없으면 서버가 시작되지 않습니다.|  
|*2*|IPv4가 옵션이고 서버가 IPv4로 수신을 시도하기는 하지만 불가능한 경우에도 서버가 시작됩니다.|  
  
 **IPV6Support**  
 IPv6 프로토콜에 대한 지원을 정의하는 부호 있는 32비트 정수 속성입니다. 이 속성은 다음 표에 나열된 값 중 하나를 가집니다.  
  
|Value|설명|  
|-----------|-----------------|  
|*0*|IPv6이 해제되어 클라이언트가 연결할 수 없습니다.|  
|*1.*|(기본값) IPv6이 필요하고 IPv6을 수신할 수 없으면 서버가 시작되지 않습니다.|  
|*2*|IPv6이 옵션이고 서버가 IPv6으로 수신을 시도하기는 하지만 불가능한 경우에도 서버가 시작됩니다.|  
  
 **MaxAllowedRequestSize**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **RequestSizeThreshold**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ServerReceiveTimeout**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ServerSendTimeout**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## 요청  
 **EnableBinaryXML**  
 서버에서 이진 xml 형식 요청을 식별하는지 여부를 지정하는 부울 속성입니다.  
  
 **EnableCompression**  
 요청에 대해 압축이 설정되어 있는지 여부를 지정하는 부울 속성입니다.  
  
## 응답  
 **CompressionLevel**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **EnableBinaryXML**  
 이진 xml 응답에 대해 서버가 설정되어 있는지 여부를 지정하는 부울 속성입니다.  
  
 **EnableCompression**  
 클라이언트 요청에 대한 응답으로 압축이 설정되어 있는지 여부를 지정하는 부울 속성입니다.  
  
## TCP  
 **InitialConnectTimeout**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MaxCompletedReceiveCount**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MaxPendingAcceptExCount**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MaxPendingReceiveCount**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MaxPendingSendCount**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MinPendingAcceptExCount**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MinPendingReceiveCount**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ScatterReceiveMultiplier**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **SocketOptions\ DisableNonblockingMode**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **SocketOptions\ EnableLingerOnClose**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **SocketOptions\EnableNagleAlgorithm**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **SocketOptions\ LingerTimeout**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **SocketOptions\ ReceiveBufferSize**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **SocketOptions\ SendBufferSize**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## 관련 항목:  
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  