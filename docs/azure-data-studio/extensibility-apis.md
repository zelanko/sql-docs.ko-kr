---
title: 확장성 API
titleSuffix: Azure Data Studio
description: Azure Data Studio에 대 한 확장성 Api에 알아봅니다
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 10ebcf94c673df4e8016ae2d0c84d7a5bd89824f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959623"
---
# <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 확장성 Api

[!INCLUDE[name-sos](../includes/name-sos.md)] 확장은 Azure Data Studio 개체 탐색기 등의 다른 부분과 상호 작용 하는 데 사용할 수 있는 API를 제공 합니다. 이러한 Api에서 사용할 수는 [ `src/sql/sqlops.d.ts` ](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.d.ts) 파일과 다음과 같습니다.

## <a name="connection-management"></a>연결 관리
`sqlops.connection`

### <a name="top-level-functions"></a>최상위 함수

- `getCurrentConnection(): Thenable<sqlops.connection.Connection>` 활성 편집기 또는 개체 탐색기 선택에 따라 현재 연결을 가져옵니다.

- `getActiveConnections(): Thenable<sqlops.connection.Connection[]>` 활성 상태인 모든 사용자 연결의 목록을 가져옵니다. 이러한 연결이 없는 경우 빈 목록을 반환 합니다.

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` 연결과 관련 된 자격 증명이 들어 있는 사전을 가져옵니다. 이러한 옵션 사전의 일부로 그렇지 않으면 반환 됩니다는 `sqlops.connection.Connection` 개체 하지만 해당 개체에서 제거 가져옵니다. 

### `Connection`
- `options: { [name: string]: string }` 연결 옵션의 사전
- `providerName: string` 연결 공급자의 이름 (예: "MSSQL")
- `connectionId: string` 연결에 대 한 고유 식별자

### <a name="example-code"></a>코드 예
```
> let connection = sqlops.connection.getCurrentConnection();
connection: {
    providerName: 'MSSQL',
    connectionId: 'd97bb63a-466e-4ef0-ab6f-00cd44721dcc',
    options: {
        server: 'mairvine-sql-server',
        user: 'sa',
        authenticationType: 'sqlLogin',
        ...
    },
    ...
}
> let credentials = sqlops.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>개체 탐색기

`sqlops.objectexplorer`


### <a name="top-level-functions"></a>최상위 함수
- `getNode(connectionId: string, nodePath?: string): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 지정 된 연결 및 경로 해당 하는 개체 탐색기 노드를 가져옵니다. 경로 지정 하는 경우 지정된 된 연결에 대 한 최상위 노드를 반환 합니다. 노드가 지정된 된 경로에서 없으면 반환 `undefined`합니다. 참고: `nodePath` 개체 SQL 도구 서비스 백 엔드에 의해 생성 되 고 손으로 생성 하기가 어렵습니다. 향후 API 개선 사항을 사용 하면 사용자가 제공한 노드의 이름, 형식 및 스키마와 같은 메타 데이터를 기반으로 노드를 가져올 수 있습니다.

- `getActiveConnectionNodes(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 모든 활성 개체 탐색기 연결 노드를 가져옵니다.

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` 지정된 된 메타 데이터와 일치 하는 모든 개체 탐색기 노드를 찾습니다. 합니다 `schema`, `database`, 및 `parentObjectNames` 인수 여야 합니다 `undefined` 있지 않은 경우 해당 합니다. `parentObjectNames` 가장 낮은 수준에서 원하는 개체 관리 되는 개체 탐색기에서 위에서 데이터베이스가 아닌 부모 개체의 목록이입니다. 예를 들어 "column1"는 테이블 "schema1.table1" 및 데이터베이스 "database1"에 속하는 열에 대 한 연결 ID를 사용 하 여 검색 하는 경우 `connectionId`, 호출 `findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`합니다. 참조를 [기본적으로 지 원하는 Azure Data Studio 형식의 목록](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API) 이 API 호출에 대 한 합니다.

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` 노드 아래에 있는 연결의 id

- `nodePath: string` 에 대 한 호출에 사용 되는 노드의 경로 `getNode` 함수입니다.

- `nodeType: string` 노드의 유형을 나타내는 문자열

- `nodeSubType: string` 하위 노드의 유형을 나타내는 문자열

- `nodeStatus: string` 노드의 상태를 나타내는 문자열

- `label: string` 개체 탐색기에서 그대로 노드에 대 한 레이블을 표시 됩니다.

- `isLeaf: boolean` 노드는 리프 노드입니다 여부 및 따라서 자식이 없습니다.

- `metadata: sqlops.ObjectMetadata` 이 노드가 나타내는 개체를 설명 하는 메타 데이터

- `errorMessage: string` 노드 오류 상태인 경우 표시 되는 메시지

- `isExpanded(): Thenable<boolean>` 개체 탐색기에서 노드가 현재 확장 되는 여부

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` 노드를 확장 하거나 축소할 수 있는지 여부를 설정 합니다. 상태는 None으로 설정 하는 경우 노드는 바뀌지 않습니다.

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` 노드가 선택 되어 있는지 여부를 설정 합니다. 경우 `clearOtherSelections` true를 새 선택 영역을 만들 때 다른 선택 항목의 선택을 취소 합니다. False 인 경우에 기존 선택 내용을 그대로 둡니다. `clearOtherSelections` 기본값은 true `selected` 때 true와 false `selected` 은 false입니다.

- `getChildren(): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` 모든 자식이 노드의 노드를 가져옵니다. 자식이 없으면 빈 목록을 반환 합니다.

- `getParent(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 이 노드의 부모 노드를 가져옵니다. 부모가 없는 경우 반환을 정의 되지 않았습니다.

### <a name="example-code"></a>코드 예

```cs
private async interactWithOENode(selectedNode: sqlops.objectexplorer.ObjectExplorerNode): Promise<void> {
    let choices = ['Expand', 'Collapse', 'Select', 'Select (multi)', 'Deselect', 'Deselect (multi)'];
    if (selectedNode.isLeaf) {
        choices[0] += ' (is leaf)';
        choices[1] += ' (is leaf)';
    } else {
        let expanded = await selectedNode.isExpanded();
        if (expanded) {
            choices[0] += ' (is expanded)';
        } else {
            choices[1] += ' (is collapsed)';
        }
    }
    let parent = await selectedNode.getParent();
    if (parent) {
        choices.push('Get Parent');
    }
    let children = await selectedNode.getChildren();
    children.forEach(child => choices.push(child.label));
    let choice = await vscode.window.showQuickPick(choices);
    let nextNode: sqlops.objectexplorer.ObjectExplorerNode = undefined;
    if (choice === choices[0]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Expanded);
    } else if (choice === choices[1]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Collapsed);
    } else if (choice === choices[2]) {
        selectedNode.setSelected(true);
    } else if (choice === choices[3]) {
        selectedNode.setSelected(true, false);
    } else if (choice === choices[4]) {
        selectedNode.setSelected(false);
    } else if (choice === choices[5]) {
        selectedNode.setSelected(false, true);
    } else if (choice === 'Get Parent') {
        nextNode = parent;
    } else {
        let childNode = children.find(child => child.label === choice);
        nextNode = childNode;
    }
    if (nextNode) {
        let updatedNode = await sqlops.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    sqlops.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>제안된 Api

대화 상자, 마법사 및 다른 기능 중 문서 탭에서 사용자 지정 UI를 표시 하려면 확장을 허용 하도록 제안 된 Api를 추가 했습니다. 참조 된 [제안 된 API 형식 파일](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.proposed.d.ts) 자세한 설명서를 통해 이러한 Api는 수 언제 든 지 변경 될 수 있습니다. 이러한 Api 중 일부를 사용 하는 방법의 예제에서 확인할 수 있습니다 합니다 ["sqlservices" 샘플 확장](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices)합니다.


