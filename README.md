# Usage
```
source s_debug {
    file(
        "/home/dme/debug_in.log"
        flags(no-parse store-raw-message)
    );
};

parser p_debug {
    msg-parser( regex('name (?P<name>\S+) prename (?P<prename>\S+)$'));
    msg-parser( regex('name: (?P<name>\S+) prename: (?P<prename>\S+)$'));
};

destination d_debug {
    file (
        "/home/dme/debug_out.log"
        #template("$(format-json --scope dot-nv-pairs)\n")
        #template(t_debug)
        template("$(format-cim)\n")
    );
};

log {
    source(s_debug);
    parse_bsd_or_ietf();
    parser(p_debug);
    destination(d_debug);
};
```
