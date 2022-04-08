# react-scroll-sync-hook

Synced scroll position across multiple scrollable elements

Originally forked from https://github.com/okonet/react-scroll-sync

## License

MIT

## Installation

```bash
npm install --save react-scroll-sync-hook
```

## Usage

```jsx

import React from 'react';
import { useRef, useMemo, useEffect } from 'react';
import { useScrollSync } from './scroll-sync';

const MyComponent = () => {
  const nodeRefA = useRef(null);
  const nodeRefB = useRef(null);
  const nodeRefC = useRef(null);

  const nodeRefs = useMemo(() => [nodeRefA, nodeRefB, nodeRefC], [nodeRefA, nodeRefB, nodeRefC]);

  const { registerPane, unregisterPane } = useScrollSync({
    // enabled, onSync, proportional, vertical, horizontal
    enabled: true,
  });

  useEffect(() => {
    nodeRefs.forEach((nodeRef) => {
      if (nodeRef?.current) {
        registerPane(nodeRef.current);
      }
    });
    return () =>
      nodeRefs.forEach((nodeRef) => {
        if (nodeRef?.current) {
          unregisterPane(nodeRef.current);
        }
      });
  }, [nodeRefs, registerPane, unregisterPane]);

  return (
    <div style={{ display: 'flex', position: 'relative', height: 300 }}>
      <div style={{ overflow: 'auto' }} ref={nodeRefA}>
        <section style={{ height: 500 }}>
          <h1>Left Pane Content</h1>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ab aperiam doloribus dolorum
            est eum eveniet exercitationem iste labore minus, neque nobis odit officiis omnis
            possimus quasi rerum sed soluta veritatis.
          </p>
        </section>
      </div>

      <div style={{ overflow: 'auto' }} ref={nodeRefB}>
        <section style={{ height: 1000 }}>
          <h1>Middle Pane Content</h1>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ab aperiam doloribus dolorum
            est eum eveniet exercitationem iste labore minus, neque nobis odit officiis omnis
            possimus quasi rerum sed soluta veritatis.
          </p>
        </section>
      </div>
      <div style={{ overflow: 'auto' }} ref={nodeRefC}>
        <section style={{ height: 2000 }}>
          <h1>Right Pane Content</h1>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ab aperiam doloribus dolorum
            est eum eveniet exercitationem iste labore minus, neque nobis odit officiis omnis
            possimus quasi rerum sed soluta veritatis.
          </p>
        </section>
      </div>
    </div>
  );

```
