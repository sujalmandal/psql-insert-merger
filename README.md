# psql-insert-merger
A tool to convert multiple insert statements into one insert statement with static selects with unions.

## Input 

    insert into artefact (identifier, "name", description) values ('scp-001','The guardian angel','Standing guard infront of what seems like a garden, it towers over the landscape at about 100 meters tall, destroying any object approaching it');

    insert into artefact (identifier, "name", description) values ('scp-049','The indestructible reptile','A seemingly indestructible crockodile like animal with insane healing capabilities. Nothing seems to kill it off completely');

## Output

    insert into artefact (identifier, "name", description) 
    select identifier, "name", description 
    from (
    
    select 'scp-001' identifier,
    'The guardian angel' "name",
    'Standing guard infront of what seems like a garden, it towers over the landscape at about 100 meters tall, destroying any object approaching it' description
    
    union
    
    select 'scp-049' identifier,
    'The indestructible reptile' "name",
    'A seemingly indestructible crockodile like animal with insane healing capabilities. Nothing seems to kill it off completely' description
    ) hardcoded_insert_table_alias;
