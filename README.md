# Batch-Processing-Using-Nodejs

```
// batch processing 
export const execInBatch = async <T>(
  items: T[],
  batchSize: number,
  callback: (item: T[]) => Promise<void>
) => {
  for (const batch of asChunks(items, batchSize)) {
    await callback(batch);
    await new Promise((resolve) => setTimeout(resolve, 1000));
  }
  return true;
};

// async ittertor 
export function* asChunks<T>(arr: T[], chunkSize: number) {
  let chunk = [];
  for (const item of arr) {
    chunk.push(item);
    if (chunk.length === chunkSize) {
      yield chunk;
      chunk = [];
    }
  }
  if (chunk.length > 0) {
    yield chunk;
  }
}


(async () => {

// implementation
  const items = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  const fn = async (item: number[]) => {
    console.log(item);
    return;
  };
  const data = await execInBatch(items, 2, fn);
  console.log(data);
})();


```
