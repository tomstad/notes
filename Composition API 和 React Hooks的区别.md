
- 前者的setup 只调用一次， 后者可以调用多次
- 前者没有 useMemo、useCallback，因为setup只执行一次
- 前者无须考虑顺序，而后者需要保证 hooks 的顺序一致
- 前者的reactive + ref 比后者的setState，更难理解