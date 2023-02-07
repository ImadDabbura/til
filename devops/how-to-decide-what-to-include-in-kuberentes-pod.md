If containers work correctly if they land on different machines, then it is
safe to include them in different pods; otherwise, they have to be in the same
pod. For example, if two containers interact through local filesystem, then it would
be impossible to operate correctly if they land on different machines.
