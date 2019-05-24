## Partner A: White Boarding

## Sorts

### Binary Search

Write a method that binary searches an array for a target and returns its
index if found. Assume a sorted array.

NB: YOU MUST WRITE THIS RECURSIVELY (searching half of the array every time).
We will not give you points if you visit every element in the array every time
you search.

For example, given the array [1, 2, 3, 4], you should NOT be checking
1 first, then 2, then 3, then 4.

def bsearch(array, target)
    return nil if array.empty?

    mid_idx = array.length / 2

    case target <=> array[mid_idx]
        when -1
            bsearch(array.take(mid_idx), target)
        when 0
            mid_idx
        when 1
            right_bsearch = bsearch(array.drop(mid_idx + 1), target)
            right_bsearch.nil? ? nil : right_bsearch + 1 + mid_idx
        end
    end
end


## Monkey Patching

### my_each

Write a method that calls a passed block for each element of the array

class Array

    def my_each(&prc)

        i = 0
        while i < self.length
            prc.call(self[i])

            i += 1
        end

        self
    end

end