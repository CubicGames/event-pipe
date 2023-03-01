# State Of The Art

## eventeum

```mermaid

classDiagram
    diretion TB
    class WebSocketService {
        WebSocketClient socketClient
        onWebSocketClose(): void
    }

    class ChainBootstraper {
        Logger log
        SubscriptionService subscriptionService
        EventFilterConfiguration filterConfiguration
        onApplicationEvent(ContextRefreshedEvent event): void
        registerFilter(ContractEventFilter filter, boolean broadcast): void
    }

    class WebSocketReconnectionManager {
        reconnect(WebSocketClient client): void
    }

    class Web3jUtil {
        Map<ParameterType, TypeMapping> typeMappings
        addUintMappings(int interval, int max): void
        addUintArrayMappings(int interval, int max): void
        addIntMappings(int interval, int max): void
        addIntArrayMappings(int interval, int max): void
        addBytesMappings(int interval, int max): void
        addBytesArrayMappings(int interval, int max): void
    }

    class BloomFilterUtil {
        getBloomBits(ContractEventFilter filter): BloomFilterBits
        bloomFilterMatch(String bloomFilterHex, BloomFilterBits bitsToMatch): boolean
    }

    class Web3jService {
        Web3j web3j
        ContractEventDetailsFactory eventDetailsFactory
        AsyncTaskService asyncTaskService
        retrieveEvents(ContractEventFilter eventFilter,BigInteger startBlock, BigInteger endBlock): List<ContractEventDetails>
        registerEventListener(ContractEventFilter eventFilter,ContractEventListener eventListener): FilterSubscription
        getCurrentBlockNumber(): BigInteger
        getBlock(String blockHash, boolean fullTransactionObjects): Optional<Block>
        getEventsForFilter(ContractEventFilter filter, BigInteger blockNumber): List<ContractEventDetails>
    }

    class BlockchainServiceFactory {
        << interface >>
        create(Node node): BlockchainService
    }

    class Web3jEventParameterConverter {
        Map<String, EventParameterConverter<Type>> typeConverters
        convert(Type toConvert): EventParameter
    }

    class AsyncTaskService {
        execute(String executorName, Runnable task): void
        submit(String executorName, Callable<T> task): Future<T>
    }

    class EventStoreService {
        << interface >>
        getLatestBlock(String nodeName): Optional<LatestBlock>
        getLatestContractEvent(String eventSignature, String contractAddress): Optional<ContractEventDetails>
    }

    class TransactionMonitoringService {
        << interface >>
        registerTransactionsToMonitor(TransactionMonitoringSpec spec, boolean broadcast): void
        stopMonitoringTransactions(String id, boolean broadcast): void
    }

    class EventRetriever {
        << interface >>
        retrieveEvents(ContractEventFilter eventFilter,
                        BigInteger startBlock,
                        BigInteger endBlock,
                        Consumer<List<ContractEventDetails>> eventConsumer): void
    }

    class ContractEventFilterRepository {
        CrudRepository crudRepository
    }

    class EventeumEventBroadcaster {
        << interface >>
        broadcastEventFilterAdded(ContractEventFilter filter): void
        broadcastEventFilterRemoved(ContractEventFilter filter): void
    }

    class BlockchainEventBroadcaster {
        << interface >>
        broadcastNewBlock(BlockDetails block): void
        broadcastContractEvent(ContractEventDetails eventDetails): void
        broadcastTransaction(TransactionDetails transactionDetails): void
    }

    class SaveableEventStore {
        << interface >>
        save(ContractEventDetails contractEventDetails): void
        save(LatestBlock latestBlock): void
    }

    class NodeServices {
        String nodeName
        Web3j web3j
        BlockchainService blockchainService
        BlockSubscriptionStrategy blockSubscriptionStrategy
    }
  
```
