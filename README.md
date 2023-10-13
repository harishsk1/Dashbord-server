# Dashbord-server

<bean id="ignite.cfg" class="org.apache.ignite.configuration.IgniteConfiguration">
    <!-- Other Ignite configuration settings -->

    <property name="dataStorageConfiguration">
        <bean class="org.apache.ignite.configuration.DataStorageConfiguration">
            <property name="storagePath" value="your_storage_path" />
            <property name="storagePath" value="/path/to/ignite/wal" />
        </bean>
    </property>

    <!-- Cassandra data source configuration -->
    <property name="dataSources">
        <list>
            <bean class="org.apache.ignite.cache.store.cassandra.datasource.DataSource">
                <property name="clusterContactPoints" value="localhost" />
                <property name="port" value="9042" />
                <property name="keyspace" value="your_keyspace" />
            </bean>
        </list>
    </property>
</bean>


  ///


<bean class="org.apache.ignite.configuration.CacheConfiguration">
    <property name="name" value="yourCacheName"/>
    <property name="cacheMode" value="PARTITIONED"/>
    <!-- Other cache configuration properties -->
</bean>

<bean id="grid.cfg" class="org.apache.ignite.configuration.IgniteConfiguration">
    <!-- Other Ignite configuration settings -->
    <property name="dataStorageConfiguration">
        <bean class="org.apache.ignite.configuration.DataStorageConfiguration">
            <property name="storagePath" value="/your/cassandra/persistence/folder"/>
            <property name="storagePath" value="/your/cassandra/persistence/folder"/>
            <!-- Other Cassandra persistence settings -->
        </bean>
    </property>
</bean>



// 


<bean class="org.apache.ignite.configuration.CacheConfiguration">
    <property name="name" value="cassandraCache" />
    <property name="cacheStoreFactory">
        <bean class="org.apache.ignite.cache.store.cassandra.CassandraCacheStoreFactory">
            <property name="dataSourceBean" value="cassandraDataSource" />
        </bean>
    </property>
</bean>

<bean id="cassandraDataSource" class="org.apache.ignite.cache.store.cassandra.datasource.CassandraDataSource">
    <property name="contactPoints" value="localhost" />
    <property name="port" value="9042" />
    <property name="readConsistency" value="ONE" />
</bean>


  ///

<bean class="org.apache.ignite.configuration.CacheConfiguration">
    <property name="name" value="cassandraCache"/>
    <property name="cacheStoreFactory">
        <bean class="org.apache.ignite.cache.store.cassandra.CassandraCacheStoreFactory">
            <property name="dataSourceBean" value="cassandraDataSource"/>
        </bean>
    </property>
</bean>


///

<bean class="org.apache.ignite.configuration.IgniteConfiguration">
    <property name="cacheConfiguration">
        <list>
            <bean class="org.apache.ignite.configuration.CacheConfiguration">
                <property name="name" value="yourCacheName" />
                <property name="readThrough" value="true" />
                <property name="cacheStoreFactory">
                    <bean class="org.apache.ignite.cache.store.cassandra.CassandraCacheStoreFactory">
                        <property name="dataSourceBean" value="yourCassandraDataSourceBean" />
                    </bean>
                </property>
            </bean>
        </list>
    </property>
</bean>



///

  <bean class="org.apache.ignite.configuration.CacheConfiguration">
    <property name="name" value="cassandraCache" />
    <property name="cacheMode" value="PARTITIONED" />
    <property name="readThrough" value="true" />
    <property name="writeThrough" value="true" />
    <property name="atomicityMode" value="ATOMIC" />
    <property name="writeBehindEnabled" value="true" />
    <property name="writeBehindFlushFrequency" value="3000" />
    <property name="writeBehindFlushSize" value="10240" />
    <property name="cacheStoreFactory">
        <bean class="org.apache.ignite.cache.store.cassandra.CassandraCacheStoreFactory">
            <property name="dataSource" ref="cassandra-ds" />
            <property name="readThrough" value="true" />
            <property name="writeThrough" value="true" />
            <property name="writeBehindEnabled" value="true" />
        </bean>
    </property>
    <property name="queryEntities">
        <list>
            <bean class="org.apache.ignite.cache.QueryEntity">
                <property name="keyType" value="java.lang.String" />
                <property name="valueType" value="your.package.YourCassandraTable" />
            </bean>
        </list>
    </property>
</bean>



////

<?xml version="1.0" encoding="UTF-8"?>
<ignite>
    <bean class="org.apache.ignite.cache.store.cassandra.CassandraCacheStoreFactory">
        <property name="dataSourceBean" value="cassandraDataSource"/>
        <!-- Configure other Cassandra properties here -->
    </bean>
    
    <bean id="cassandraDataSource" class="javax.sql.DataSource">
        <!-- Cassandra DataSource configuration here -->
    </bean>
    <!-- Other Ignite configurations -->
</ignite>

////



<bean id="ignite.cfg" class="org.apache.ignite.configuration.IgniteConfiguration">
    <property name="dataStorageConfiguration">
        <bean class="org.apache.ignite.configuration.DataStorageConfiguration">
            <property name="defaultDataRegionConfiguration">
                <bean class="org.apache.ignite.configuration.DataRegionConfiguration">
                    <property name="persistenceEnabled" value="true"/>
                </bean>
            </property>
        </bean>
    </property>
    <property name="cacheConfiguration">
        <list>
            <!-- Define your cache configurations here -->
        </list>
    </property>
    <property name="includedEventTypes">
        <list>
            <util:constant static-field="org.apache.ignite.events.EventType.EVT_CACHE_OBJECT_PUT"/>
        </list>
    </property>
</bean>


